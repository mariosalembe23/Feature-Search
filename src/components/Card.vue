<template>
  <main class="w-full h-screen px-5">
    <div
      class="boxSearch relative md:max-w-xl lg:max-w-2xl w-full shadow-lg py-5 bg-zinc-800 overflow-hidden rounded-lg mt-10 mx-auto"
    >
      <header class="w-full px-5 flex items-center justify-between space-x-3">
        <div>
          <button
          @click="filterUsers"
            id="pesquisar"
            class="hover:text-green-500 transition-all relative text-green-400"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
              />
            </svg>
            <small
              class="tooltipPesquisar text-green-400 bg-zinc-900 px-4 py-2 absolute top-12 left-4 shadow-lg font-medium rounded-md"
              >Pesquisar</small
            >
          </button>
        </div>
        <div class="w-full">
          <input
            v-model="inputValue"
            @input="filterUsers"
            type="text"
            name="search"
            id="search"
            class="w-full bg-transparent py-2 outline-none border-l font-medium text-white px-3 border-zinc-700"
            placeholder="Busque Por um Nome"
          />
        </div>
        <div>
          <button
            @click="clearInput"
            id="deletar"
            class="text-zinc-400 transition-all relative hover:text-red-300"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0"
              />
            </svg>

            <small
              class="tooltipDelete text-green-400 bg-zinc-900 px-4 py-2 absolute top-12 -left-12 shadow-lg font-medium rounded-md"
              >Apagar</small
            >
          </button>
        </div>
      </header>

      <div class="flex flex-col justify-between w-full h-full overflow-hidden">
        <main class="w-full h-full overflow-auto p-3">
          <!-- IF INPUT IS EMPTY -->
          <div
            v-if="inputValue === ''"
            class="w-full h-full flex items-center justify-center text-center"
          >
            <div class="flex items-center gap-2 flex-wrap justify-center">
              <p class="font-semibold text-zinc-300" id="textInitial">
                {{ text }}
              </p>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-6 h-6 text-zinc-300 iconInitial"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M15 9h3.75M15 12h3.75M15 15h3.75M4.5 19.5h15a2.25 2.25 0 002.25-2.25V6.75A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25v10.5A2.25 2.25 0 004.5 19.5zm6-10.125a1.875 1.875 0 11-3.75 0 1.875 1.875 0 013.75 0zm1.294 6.336a6.721 6.721 0 01-3.17.789 6.721 6.721 0 01-3.168-.789 3.376 3.376 0 016.338 0z"
                />
              </svg>
            </div>
          </div>

          <!-- DATA LAUDING -->
          <div
          v-if="dataLouding"
          class="w-full h-full flex items-center justify-center text-center"
        >
          <div class="flex items-center gap-2 flex-wrap justify-center">
            <p class="font-semibold text-zinc-300" id="textInitial">
              Aguarde...
            </p>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-6 h-6 text-zinc-300 iconInitial"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M15 9h3.75M15 12h3.75M15 15h3.75M4.5 19.5h15a2.25 2.25 0 002.25-2.25V6.75A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25v10.5A2.25 2.25 0 004.5 19.5zm6-10.125a1.875 1.875 0 11-3.75 0 1.875 1.875 0 013.75 0zm1.294 6.336a6.721 6.721 0 01-3.17.789 6.721 6.721 0 01-3.168-.789 3.376 3.376 0 016.338 0z"
              />
            </svg>
          </div>
        </div>
          <!-- SEM RESULTADOS -->
          <div
            v-if="dataNotFound === true"
            class="w-full h-full flex items-center justify-center text-center"
          >
            <div class="flex items-center gap-2 flex-wrap justify-center">
              <p class="font-semibold text-zinc-500">Nenhum Dado Encontrado</p>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="currentColor"
                class="bi bi-app-indicator w-6 h-6 text-zinc-500"
                viewBox="0 0 16 16"
              >
                <path
                  d="M5.5 2A3.5 3.5 0 0 0 2 5.5v5A3.5 3.5 0 0 0 5.5 14h5a3.5 3.5 0 0 0 3.5-3.5V8a.5.5 0 0 1 1 0v2.5a4.5 4.5 0 0 1-4.5 4.5h-5A4.5 4.5 0 0 1 1 10.5v-5A4.5 4.5 0 0 1 5.5 1H8a.5.5 0 0 1 0 1H5.5z"
                />
                <path d="M16 3a3 3 0 1 1-6 0 3 3 0 0 1 6 0z" />
              </svg>
            </div>
          </div>

          <!-- IF HAS A RESULT -->
          <div
            v-if="inputValue !== ''"
            class="userResult grid w-full grid-cols-1 gap-7 p-5 mt-3 items-start"
          >
            <!-- USERS -->
            <li
              v-for="item in users"
              class="list-none w-full flex items-center justify-between cursor-pointer itemUser"
            >
              <div class="flex items-center w-full space-x-3">
                <div>
                  <div
                    class="image w-11 h-11 shadow-lg rounded-full"
                    :style="{ background: item.imageColor }"
                  ></div>
                </div>
                <div class="infoUsers space-y-1">
                  <h4 class="nameUser text-white font-medium">
                    <!-- ESTA NÃO É UMA PRÁTICA ACONSELHÁVEL, USE PROPRIEDADES COMPUTADAS!!! -->
                    {{ item.firstName }} {{ item.apelido }}
                  </h4>
                  <p class="states text-zinc-400">{{ item.funcao }}</p>
                </div>
              </div>
              <a
                href="#"
                class="linkChamar hidden md:inline-block text-white bg-zinc-900 rounded-full px-4 py-1 font-medium transition-all hover:bg-green-400 hover:text-zinc-900"
                >chamar</a
              >
            </li>
          </div>
        </main>

        <!-- FOOTER -->
        <footer
          class="w-full h-20 flex items-start py-3 px-4 border-t border-zinc-700 bg-zinc-800"
        >
          <div
            class="w-full flex items-center md:justify-between justify-center"
          >
            <a
              href="https://github.com/mariosalembe23"
              class="me hidden md:inline-block text-zinc-500 font-medium transition-all hover:text-green-400"
              >Mário Salembe Dev.</a
            >
            <small class="text-green-400 font-medium">&copy;Morphosis</small>
          </div>
        </footer>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      item: 0,
      users: [],
      inputValue: "",
      dataNotFound: null,
      text: "Inicie Sua Pesquisa para Obter Resultados...",
      dataLouding: false,
    };
  },
  methods: {
    clearInput() {
      this.inputValue = "";
      this.dataNotFound = true;
    },

    async filterUsers(e) {
      // PEGANDO VALOR DO MESMO INPUT
      const valueInput = e.target.value;
      const query = valueInput.toLowerCase();
      const ifInputIsEmpty = valueInput.length !== 0;
      if (ifInputIsEmpty) {
        this.dataLouding = true;
        try {
          // FAZENDO A REQUISIÇÃO
          const request = await axios.get(
            "https://json-api-fswv.onrender.com/users"
          );
          const data = await request.data;

          // TRANSFORMANDO UM OBJECT EM UM ARRAY
          const dataArray = Array.isArray(data) ? data : [data];

          const userFound = dataArray.filter(
            (user) =>
              user.firstName.toLowerCase().startsWith(query) ||
              user.firstName.toLowerCase() === query ||
              user.apelido.toLowerCase().startsWith(query) ||
              user.apelido.toLowerCase() === query
          );
          this.dataLouding = false;
          if (userFound.length === 0) {
            this.dataNotFound = true;
          } else {
            this.dataNotFound = false;
          }
          this.users = userFound;
        } catch (error) {
          console.error("Ocorreu um erro:" + error);
        }
      } else {
        this.inputValue = "";
      }
    },
  },
};
</script>

<style scoped>
.me {
  font-size: 14px;
}
.linkChamar {
  font-size: 14px;
  display: none;
}

.states {
  font-size: 14px;
}
.nameUser {
  font-family: "Poppins", sans-serif;
  font-size: 15px;
}
input {
  font-family: "Poppins", sans-serif;
  font-size: 15px;
}
.tooltipPesquisar,
.tooltipDelete {
  display: none;
}
#pesquisar:hover .tooltipPesquisar {
  display: inline-block;
}
#deletar:hover .tooltipDelete {
  display: inline-block;
}
.boxSearch {
  height: 29rem;
}
#textInitial,
.iconInitial {
  transition: all 0.15s ease-in-out;
  animation: opacidade 1s ease-in-out alternate infinite;
}

@keyframes opacidade {
  from {
    opacity: 0.2;
  }
  to {
    opacity: 1;
  }
}

@media screen and (min-width: 640px) {
  .itemUser:hover .linkChamar {
    display: inline-block;
  }
}
</style>
