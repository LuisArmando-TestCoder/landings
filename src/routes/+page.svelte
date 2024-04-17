<script>
    export let name = "";
</script>

<main>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/8.0.1/normalize.min.css">

    <h1>
        soft
        <br>
        smooth
        <br>
        & tasty
    </h1>

    <h2>Libre Baskervile</h2>

    <hr>

    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Nulla nostrum eveniet similique nihil ullam id explicabo aperiam voluptas. A, dolorum itaque minus deleniti facilis rerum suscipit fugiat distinctio ipsam recusandae.</p>
</main>

<style>
    /* static/fonts.css */

    /* League Spartan */
    @font-face {
        font-family: 'League Spartan';
        font-weight: bold;
        src: url('/fonts/League_Spartan/static/LeagueSpartan-Black.ttf') format('truetype');
    }

    /* Libre Baskervile */
    @font-face {
        font-family: 'Libre Baskervile';
        font-weight: normal;
        src: url('/fonts/Libre_Baskerville/LibreBaskerville-Regular.ttf') format('truetype');
    }

    /* Poppins */
    @font-face {
        font-family: 'Poppins Light';
        font-weight: normal;
        src: url('/fonts/Poppins/Poppins-Light.ttf') format('truetype');
    }

    :root {
        --color-foreground: #22223b;
        --color-outline: #4a4e69;
        --color-highlight-1: #9a8c98;
        --color-highlight-1: #c9ada7;
        --color-background: #f2e9e4;

        --font-title: 'League Spartan', serif;
        --font-subtitle: 'Libre Baskervile', serif;
        --font-paragraph: 'Poppins Light', sans-serif;
    }

    h1 {
        font-family: var(--font-title);
        font-size: clamp(30px, 40vw, 130px);
    }

    h2, h3, h4, h5 {
        font-family: var(--font-subtitle);
        font-weight: 100;
        text-transform: uppercase;
        font-size: 24px;
        letter-spacing: 7px;
    }

    p {
        font-family: var(--font-paragraph);
        max-width: 450px;
    }
</style>
