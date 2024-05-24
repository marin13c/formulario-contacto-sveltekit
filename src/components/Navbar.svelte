<script>
// @ts-nocheck

    // Función para mostrar/ocultar el menú móvil
    function toggleMobileMenu() {
      const mobileMenu = document.getElementById("mobile-menu");
      const menuButton = document.querySelector(
        'button[aria-controls="mobile-menu"]'
      );
      const expanded = menuButton.getAttribute("aria-expanded") === "true";
  
      if (expanded) {
        mobileMenu.classList.remove("block");
        mobileMenu.classList.add("hidden");
        menuButton.setAttribute("aria-expanded", "false");
      } else {
        mobileMenu.classList.remove("hidden");
        mobileMenu.classList.add("block");
        menuButton.setAttribute("aria-expanded", "true");
      }
    }
</script>
<nav>
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
      <div class="relative flex h-16 items-center justify-between">
        <div
          class="flex flex-1 items-center justify-center sm:items-stretch sm:justify-start"
        >
          <!-- Botón para el menú móvil -->
          <button
            type="button"
            class="inline-flex items-center justify-center rounded-md p-2 text-gray-400 hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white sm:hidden"
            aria-controls="mobile-menu"
            aria-expanded="false"
            on:click={toggleMobileMenu}
          >
            <span class="sr-only">Open main menu</span>
            <!-- Icono de menú (tres barras) -->
            <svg
              class="block h-6 w-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M4 6h16M4 12h16M4 18h16"
              ></path>
            </svg>
            <!-- Icono de cerrar menú (X) -->
            <svg
              class="hidden h-6 w-6"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              aria-hidden="true"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M6 18L18 6M6 6l12 12"
              ></path>
            </svg>
          </button>
          <!-- Menú principal en pantallas grandes -->
          <div class="hidden sm:ml-6 sm:block">
            <div class="flex space-x-4">
              <a
                href="#"
                class="text-white hover:text-gray-500 rounded-md px-3 py-2 text-sm font-medium"
                aria-current="page">Home</a
              >
              <a
                href="#"
                class="text-white hover:text-gray-500 rounded-md px-3 py-2 text-sm font-medium flex items-center"
              >
                Services
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-4 w-4 ml-1"
                  viewBox="0 0 20 20"
                  fill="#ffffff"
                >
                  <path d="M10 12l-5-5h10l-5 5z"></path>
                </svg>
              </a>
              <a
                href="#"
                class="text-white hover:text-gray-500 rounded-md px-3 py-2 text-sm font-medium flex items-center"
              >
                About Us
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-4 w-4 ml-1"
                  viewBox="0 0 20 20"
                  fill="#ffffff"
                >
                  <path d="M10 12l-5-5h10l-5 5z"></path>
                </svg>
              </a>
              <a
                href="#"
                class="text-white hover:text-gray-500 rounded-md px-3 py-2 text-sm font-medium"
                >Pricing</a
              >
            </div>
          </div>
        </div>
        <!-- Botón Apply -->
        <div
          class="absolute inset-y-0 right-0 flex items-center pr-2 sm:static sm:inset-auto sm:ml-6 sm:pr-0"
        >
          <li>
            <a
              href="#"
              class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
              >Apply</a
            >
          </li>
        </div>
      </div>
    </div>
  
    <!-- Menú móvil -->
    <div class="sm:hidden hidden" id="mobile-menu">
      <div class="px-2 pt-2 pb-3 space-y-1">
        <a
          href="#"
          class="text-gray-300 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-medium"
          >Home</a
        >
        <a
          href="#"
          class="text-gray-300 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-medium"
          >Services</a
        >
        <a
          href="#"
          class="text-gray-300 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-medium"
          >About Us</a
        >
        <a
          href="#"
          class="text-gray-300 hover:bg-gray-700 hover:text-white block px-3 py-2 rounded-md text-base font-medium"
          >Pricing</a
        >
      </div>
    </div>
  </nav>