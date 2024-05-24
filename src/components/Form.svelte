<script>
// @ts-nocheck

  import { onMount } from "svelte";
  import servicesData from "../JSONFRONTEND.json";
  import Modal from './Modal.svelte'; // Importa el componente de modal
  
  let registers = {
    name: "",
    last_name: "",
    email: "",
    phone: "",
    message: "",
    services: [],
  };

  // @ts-ignore
  let selectedCategory = [];
  // @ts-ignore
  let filteredServices = [];
  let showModal = false;
  let successMessage = false;
  let isServicesEmpty = registers.services.length === 0;
  let selectedCategories = new Set();
  // @ts-ignore
  let hoveredService = null;

  // @ts-ignore
  const toggleService = (service) => {
    // Función para agregar o quitar un servicio de la lista de servicios seleccionados
    // @ts-ignore
    if (registers.services.includes(service.nombre)) {
      registers.services = registers.services.filter(
        (s) => s !== service.nombre
      );
    } else {
      // @ts-ignore
      registers.services = [...registers.services, service.nombre];
    }
  };

  // @ts-ignore
  const toggleCategory = (category) => {
    // Función para agregar o quitar una categoría de la lista de categorías seleccionadas
    if (selectedCategories.has(category)) {
      selectedCategories.delete(category);
    } else {
      selectedCategories.add(category);
    }
    filterByCategory(); // Filtra los servicios según las categorías seleccionadas
  };

  const filterByCategory = () => {
    // Función para filtrar servicios según las categorías seleccionadas
    filteredServices = servicesData.servicios.filter((service) => {
      if (selectedCategory.length === 0) return true;
      return (
        // @ts-ignore
        selectedCategory.includes("") ||
        // @ts-ignore
        selectedCategory.some((category) =>
          service.categorias.includes(category)
        )
      );
    });
  };

  onMount(() => {
    registers.services = [];
    filterByCategory(); // Filtra los servicios al montar el componente
  });

  // @ts-ignore
  const onSubmitHandler = async (e) => {
    e.preventDefault();
    console.log(registers);

    const isEmpty = Object.values(registers).some((val) => val === "");
    const isServicesEmpty = registers.services.length === 0;

    if (isEmpty || isServicesEmpty) {
      successMessage = false;
      showModal = true;
      return;
    }
    try {
      const response = await fetch("https://sheetdb.io/api/v1/odjc84c2k7kvc", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(registers),
      });

      if (response.ok) {
        console.log("Data successfully sent");
        showModal = true;
        successMessage = true;
      } else {
        console.error("Error sending data");
      }
    } catch (error) {
      console.error("Error sending data:", error);
    }
  };
  

  let handleCloseModal = () => {
    showModal = false;
    if (successMessage) {
      window.location.reload();
    }
  };

  const uniqueCategories = Array.from(
    new Set(servicesData.servicios.flatMap((service) => service.categorias))
  );
</script>

<main class="mainform">
  <form
    class="form"
    on:submit={onSubmitHandler}
  >
    <!-- Contenido del formulario... -->
    <div
    class="text-3xl sm:text-4xl lg:text-6xl font-semibold leading-tight mb-4 font-bb-casual-pro-medium text-gradient"
    style="text-align: left;"
  >
    Contact Us
  </div>
  <div
    class="text-xl sm:text-2xl lg:text-4xl font-semibold leading-tight mb-4 text-white font-bb-casual-pro-medium"
    style="text-align: left"
  >
    Let us know what you need
  </div>
  <div class="leading-tight mb-4 text-white" style="text-align: left">
    Please fill all these spaces, for us to reach you with the best quote.
  </div>
  <div class="mb-4 flex flex-col sm:flex-row">
    <div class="w-full sm:w-3/5 sm:pr-2 mb-4 sm:mb-0">
      <!-- Campo para el nombre -->
      <label class="labelform" for="name"
        >First Name</label
      >
      <input
        class="inputs"
        bind:value={registers.name}
        type="text"
        id="name"
      />
    </div>
    <div class="w-full sm:w-2/5 sm:pl-2">
      <!-- Campo para el apellido -->
      <label class="labelform" for="last_name"
        >Last Name</label
      >
      <input
        class="inputs"
        bind:value={registers.last_name}
        type="text"
        id="last_name"
      />
    </div>
  </div>
  <div class="mb-4">
    <!-- Campo para el correo electrónico -->
    <label class="labelform" for="email"
      >Email</label
    >
    <input
      class="inputs"
      bind:value={registers.email}
      type="text"
      id="email"
    />
  </div>
  <div class="mb-4">
    <!-- Campo para el teléfono -->
    <label class="labelform" for="phone"
      >Phone</label
    >
    <input
      class="inputs"
      bind:value={registers.phone}
      type="text"
      id="phone"
    />
  </div>
  <div class="mb-4">
    <!-- Campo para el mensaje -->
    <label class="labelform" for="message"
      >Message</label
    >
    <textarea
      class="inputs"
      bind:value={registers.message}
      id="message"
      rows="5"
    ></textarea>
  </div>
  <div class="mb-4">
    <!-- Selección de servicios -->

    <label class="labelform" for="services"
      >Filter by category</label
    >
    <select
      class="inputs"
      bind:value={selectedCategory}
      multiple
      on:change={toggleCategory}
    >
      <option value="">All Categories</option>
      {#each uniqueCategories as category}
        <option value={category}>{category}</option>
      {/each}
    </select>

    <!-- Lista de servicios filtrados con checkbox -->

    <label class="labelform" for="services"
      >Services</label
    >
    {#each filteredServices as service}
      <div class="mb-2 relative">
        <input
          type="checkbox"
          id={service.nombre}
          checked={registers.services.includes(service.nombre)}
          on:change={() => toggleService(service)}
          class="mr-2 leading-tight"
        />
        <label
          for={service.nombre}
          class="text-white text-sm"
          on:mouseenter={() => (hoveredService = service)}
          on:mouseleave={() => (hoveredService = null)}
        >
          {service.nombre}
        </label>
        <!-- Tooltip que muestra la descripción y precio del servicio -->
        {#if hoveredService && hoveredService.nombre === service.nombre}
          <div
            class="absolute bg-white text-black text-sm p-2 rounded shadow-lg"
            style="left: 15rem; top: 0;"
          >
            {hoveredService.descripcion} ({hoveredService.precio})
          </div>
        {/if}
      </div>
    {/each}

    <!-- Botón para enviar el formulario -->

    <div class="flex items-center justify-between mt-4">
      <button
        class="custom-button"
        type="submit"
      >
        Get started
      </button>
    </div>
  </form>

  <!-- Componente Modal -->

  <Modal
  bind:showModal={showModal}
  bind:successMessage={successMessage}
  bind:registers={registers}
  bind:handleCloseModal={handleCloseModal}
  bind:isServicesEmpty={isServicesEmpty}
/>
</main>
