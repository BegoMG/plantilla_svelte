
<script>

  import { onMount } from 'svelte';

  import imagenMov from "../assets/img/im1.jpg";
  import imagenTab from "../assets/img/im1.jpg";
  import imagenDesk1 from "../assets/img/im2.jpg";
  import imagenDesk2 from "../assets/img/im2.jpg";


/*
  import videoMov from "../assets/img/video_movil.jpg";
  import videoTab from "../assets/img/video_tablet.jpg";
  import videoDesk1 from "../assets/img/video_desk1.jpg";
  import videoDesk2 from "../assets/img/video_desk2.jpg"; 
*/

  let tipoFondo = "imagen"; // o "video"



  let imgSource = imagenMov; // Valor per defecte
  let videoSource;


//OJU Si obrim amb vídeo, s'haurien de canviar les variables:
  function actualizarSource(){
    const width = window.innerWidth;

    if (width <= 550) {
      imgSource = imagenMov; //sería videoSource = videoMov, etc
    } else if (width <= 950) {
      imgSource = imagenTab;
    } else if (width <= 1200) {
      imgSource = imagenDesk1;
    } else {
      imgSource = imagenDesk2;
    }
  }

  onMount(() => {
    actualizarSource();
    window.addEventListener("resize", actualizarSource);

    return () => {
      window.removeEventListener("resize", actualizarSource);
    };
  });



</script>









<section class="lv_jumbo">
  {#if tipoFondo === "imagen"}
    <img class="lv_jumbo-bg" src={imgSource} alt="fondo jumbo" />
  {:else if tipoFondo === "video"}
    <video class="lv_jumbo-bg" autoplay muted loop playsinline>
      <source src={videoSource} type="video/mp4" />
    </video>
  {/if}

  <div class="lv_jumbo-content">
    <h1 class="lv_jumbo-title">Título del reportaje</h1>
    <p class="lv_jumbo-subtitle">Subtítulo opcional</p>
  </div>

  <div class="lv_scrollIcon"><span></span></div>
</section>








<style>
  .lv_jumbo {
    position: relative;
    width: 100vw;
    height: 100dvh;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
  }

  .lv_jumbo-bg {
    position: absolute;
    inset: 0;
    object-fit: cover;
    width: 100%;
    height: 100%;
    z-index: 0;
  }

  .lv_jumbo-content {
    position: relative;
    z-index: 1;
    color: white;
    padding:20px;
    background-color: rgba(0, 0, 0, 0.5);
  }

  .lv_jumbo-title{
    margin: 0;
    font-family:"HBold", serif;
    font-size: 35px;
    text-shadow: 0 2px 5px rgba(0, 0, 0, 0.5);
  }

  .lv_jumbo-subtitle{
    font-family:"TRegular", serif;
    font-size: 18px;
    margin-top: 0.5rem;
    text-shadow: 0 2px 5px rgba(0, 0, 0, 0.5);
  }




  /* Icono scroll */

    .lv_scrollIcon {
        width: 80px;
        height: 80px;
        position: absolute;
        bottom: 5%;
        left: 50%;
        transform: translateX(-50%);
        z-index: 4;
      }

    .lv_scrollIcon span {
      display: block;
      width: 100%;
      height: 100%;
      background-image: url('https://visuals.lavanguardia.com/otros/icons/flechaScrollFinaNegra.png');
      /* background-image: url('https://visuals.lavanguardia.com/otros/icons/flechaScrollFinaBlanca.png'); */
      /* background-image: url('https://visuals.lavanguardia.com/otros/icons/flechaScrollFinaAzul.png'); */
      /* background-image: url('https://visuals.lavanguardia.com/otros/icons/flechaScrollFinaGris.png'); */
      background-size: contain;
      background-position: center;
      animation: lv_parpadeo 2s ease-in-out infinite;
    }

    @keyframes lv_parpadeo {
      0%, 100% { opacity: 0.2; }
      50% { opacity: 1; }
    }




    /* Media queries */


    @media (min-width: 750px){

        .lv_jumbo-title {
            font-size: 46px;
        }


    } 



    @media (min-width: 950px){

        .lv_jumbo-title {
            font-size: 51px;
        }

          .lv_jumbo-subtitle{
            font-size: 19px;
          }

        .lv_scrollIcon span {
          background-image: url('https://visuals.lavanguardia.com/otros/icons/flechaScrollGruesaNegra.png');
          /* background-image: url('https://visuals.lavanguardia.com/otros/icons/flechaScrollGruesaBlanca.png'); */
          /* background-image: url('https://visuals.lavanguardia.com/otros/icons/flechaScrollGruesaAzul.png'); */
          /* background-image: url('https://visuals.lavanguardia.com/otros/icons/flechaScrollGruesaGris.png'); */
        }

        .lv_scrollIcon {
          width: 100px;
          height: 100px;
        }


    } 




    @media (min-width: 1200px){

        .lv_jumbo-title {
            font-size: 56px;
        }

          .lv_jumbo-subtitle{
            font-size: 20px;
          }


    } 







</style>