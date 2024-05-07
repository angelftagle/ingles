<template>
  <div id="app">
    <!-- Header -->
    <header>
      <div class="logo">
        <img src="@/assets/site-logo.jpg" alt="Logo de Gogru Ingles">
      </div>
      <nav>
        <ul>
          <li><a href="#">Inicio</a></li>
          <li><a href="#">Cursos</a></li>
          <li><a href="#">Horarios</a></li>
          <li><a href="#">Contacto</a></li>
        </ul>
      </nav>
      <div class="redes-sociales">
              <social-share-network
                v-for="network in networks"
                :network="network"
                :key="network"
                url="https://gogruingles.com"
                title="{{ network }}"
                description="¡Descubre cómo mejorar tu inglés en Gogru Ingles!">
                <img :src="`/src/assets/networks/${network}.png`" alt="Compartir en {{ network }}">
                <br>
              </social-share-network>

      </div>
    </header>

    <!-- Body -->
    <main>
      <Slider/>
      <div class="contenido">
        <!-- Foro de preguntas frecuentes -->
        <div class="faq">
          <h2>Preguntas Frecuentes</h2>
          <ul>
            <li><a href="#">¿Cómo me inscribo en un curso?</a></li>
            <li><a href="#">¿Cuáles son los horarios de clases?</a></li>
            <li><a href="#">¿Cómo puedo contactar al profesor?</a></li>
          </ul>
        </div>
        <!-- Chat -->
        <div class="chat">
            <h2>Chat en Vivo</h2>
            <div class="chat-messages">
              <div v-for="(message, index) in messages" :key="index" class="message">
                <strong>{{ message.sender }}:</strong> {{ message.text }}
              </div>
            </div>
            <div class="chat-input">
              <input type="text" v-model="newMessage" @keyup.enter="sendMessage" placeholder="Escribe tu mensaje aquí...">
              <button @click="sendMessage">Enviar</button>
            </div>
          </div>


      </div>
      <div>
        <vue-plyr>
          <div class="video-wrapper"
          data-plyr-provider="youtube" 
          data-plyr-embed-id="bTqVqk7FSmY">
          </div>
        </vue-plyr>
      </div>
      <br><br><br>
      <div>
        <button @click="isVisible = !isVisible">ANIMACION EMBEBIDA</button>
        <transition name="fade">
          <img src="@/assets/esc_ing.gif"  v-if="isVisible">
        </transition>
      </div>

      
        <div class="signupFrm">
          <form action="" class="form">
            <h1 class="title">Formulario</h1>

            <div class="inputContainer">
              <input type="text" class="input" placeholder="Ingresa tu Email">
              <label for="" class="label">Email</label>
            </div>

            <div class="inputContainer">
              <input type="text" class="input" placeholder="Ingresa tu usuario">
              <label for="" class="label">Usuario</label>
            </div>

            <div class="inputContainer">
              <input type="text" class="input" placeholder="Ingresa tu contraseña">
              <label for="" class="label">Contraseña</label>
            </div>

            <div class="inputContainer">
              <input type="text" class="input" placeholder="Confirma tu contraseña">
              <label for="" class="label">Confirma tu Contraseña</label>
            </div>

            <input type="submit" class="submitBtn" value="Registrar">
          </form>
        </div>  

        <GoogleMap
        api-key="AIzaSyDp3Ud3SixagW8bJOwtosy5bBMB5JRNS_k"
        style="width: 100%; height: 500px"
        :center="center"
        :zoom="15"
        >
          <Marker :options="{ position: center }" />
        </GoogleMap>
        <br>
        <h1>Ubicación
        </h1>
        <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3763.1888673209605!2d-99.11598792415674!3d19.404243941584664!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d1ff4c147cff73%3A0xb999a5d2e9b6a002!2sFrancisco%20del%20paso%20Residencial!5e0!3m2!1ses-419!2smx!4v1714975422023!5m2!1ses-419!2smx" width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>

        <br>

        
        
        
    </main>

    <!-- Footer -->
    <footer>
      <div class="rating">
        <h2>Valoración de la página</h2>
        <div class="stars">
          <span v-for="star in 5" :key="star" @click="ratePage(star)" :class="{ 'rated': star <= currentPageRating }">&#9733;</span>
        </div>
        <p>Has valorado esta página con {{ currentPageRating }} estrellas</p>
      </div>
      <p>Contacto: <a href="mailto:info@gogruingles.com">info@gogruingles.com</a> | Teléfono: 123-456-7890</p>
    </footer>
  </div>

</template>

<script>
import { SocialShareNetwork } from 'vue-social-sharing';
import VueRate from 'vue-rate';
import Slider from "@/components/Slider.vue";
import { GoogleMap, Marker } from 'vue3-google-map'

const center = { lat: 40.689247, lng: -74.044502 }



export default {
  data() {
    return {
      networks: ['facebook', 'twitter', 'instagram','wa'],
      messages: [],
            newMessage: '',
      rating: 0,
      currentIndex: 0, // Índice actual de la imagen en el slider
      currentPageRating: 0, // Valoración actual de la página
      isVisible: false
    };
  },
  components: {
    Slider,
    SocialShareNetwork,
    VueRate
  },
  methods: {
      sendMessage() {
        if (this.newMessage.trim() !== '') {
          this.messages.push({ sender: 'Tú', text: this.newMessage });
          this.newMessage = ''; // Limpiar el campo de entrada después de enviar el mensaje
        }
      },
    onRatingChanged(newValue) {
      // Este método se ejecuta cuando el usuario cambia la puntuación
      console.log('Nueva puntuación:', newValue);
    },
    ratePage(stars) {
      this.currentPageRating = stars;
    }
    }
};
</script>


<style scoped>

#app {
  font-family: Arial, sans-serif;
  color: #333; /* Color de texto gris oscuro */
}

header {
    background-color: #1c3961; /* Azul de fondo */
    color: white;
    padding: 10px 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.logo {
    display: flex;
    align-items: center;
}

.logo img {
    width: 250px;
    height: auto;
    margin-right: 10px;
}

.logo h1 {
    margin: 0;
}

.redes-sociales img {
    width: 30px;
    height: 30px;
    cursor: pointer;
}

nav ul {
    list-style-type: none;
    display: flex;
}

nav ul li {
    margin-right: 20px;
}

main {
    padding: 20px;
}

.contenido {
    display: flex;
}

.faq {
    flex: 1;
    background-color: #f8f9fa; /* Gris claro */
    padding: 20px;
}

.faq h2 {
    color: #333; /* Texto gris oscuro */
}

.faq ul {
    list-style-type: none;
    padding: 0;
}

.faq ul li {
    margin-bottom: 10px;
}

.chat {
    flex: 1;
    background-color: #f8f9fa; /* Gris claro */
    padding: 20px;
}

footer {
    background-color: #1c3961; /* Azul */
    color: white;
    padding: 10px 20px;
    text-align: center;
}

.chat {
  border: 1px solid #ccc;
  padding: 20px;
  border-radius: 5px;
}

.chat h2 {
  margin-top: 0;
}

.chat-messages {
  max-height: 200px;
  overflow-y: auto;
}

.message {
  margin-bottom: 5px;
}

.chat-input {
  margin-top: 10px;
}

.chat-input input {
  width: 80%;
  padding: 5px;
}

.chat-input button {
  width: 30%;
  padding: 5px;
}

.carousel-container {
  max-width: 800px; /* Ancho máximo del carrusel */
  margin: 0 auto; /* Centrar el carrusel */
}
/* Estilos para la valoración de la página */
.rating {
  margin-top: 20px;
}

.rating h2 {
  margin-bottom: 10px;
}

.stars {
  font-size: 30px;
}

.stars span {
  cursor: pointer;
  color: #ccc;
  transition: color 0.3s;
}

.stars span.rated {
  color: #ffc107; /* Color de estrella seleccionada */
}

.video-wrapper{
  width: 20%;
  }

  .signupFrm {
  display: flex;
  justify-content: center;
  align-items: center;
}

.form {
  background-color: white;
  width: 400px;
  border-radius: 8px;
  padding: 20px 40px;
  box-shadow: 0 10px 25px rgba(92, 99, 105, .2);
}

.title {
  font-size: 50px;
  margin-bottom: 50px;
}

.inputContainer {
  position: relative;
  height: 45px;
  width: 90%;
  margin-bottom: 17px;
}

.input {
  position: absolute;
  top: 0px;
  left: 0px;
  height: 100%;
  width: 100%;
  border: 1px solid #DADCE0;
  border-radius: 7px;
  font-size: 16px;
  padding: 0 20px;
  outline: none;
  background: none;
  z-index: 1;
}

.label {
  position: absolute;
  top: 15px;
  left: 15px;
  padding: 0 4px;
  background-color: white;
  color: #DADCE0;
  font-size: 16px;
  transition: 0.5s;
  z-index: 0;
}

.submitBtn {
  display: block;
  margin-left: auto;
  padding: 15px 30px;
  border: none;
  background-color: purple;
  color: white;
  border-radius: 6px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 30px;
}

.submitBtn:hover {
  background-color: #9867C5;
  transform: translateY(-2px);
}

/* Hide the placeholder texts (a) */

::placeholder {
  color: transparent;
}

.fade-enter-active, .fade-leave-active {
     transition: opacity 0.5s;
}
 .fade-enter, .fade-leave-to {
     opacity: 0;
}
 
</style>
