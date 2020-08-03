<template>
    <body>
        <div class="clock">
            <div class="hour"></div>
            <div class="min"></div>
            <div class="sec"></div>
        </div>
    </body>
</template>

<style>
    *{
    margin: 0;
    padding: 0;
    box-sizing: border-box; /*définit la façon dont la hauteur et la largeur totale d'un élément est calculée*/
    }
    body{
        display: flex;
        justify-content: center;
        align-items: center;
        /*min-height: 100vh;*/
        background-color: #091921;
    }

    .clock{
        width: 400px;
        height: 400px;
        display: flex;
        justify-content: center;
        align-items: center;
        background: url(../assets/clock.png);
        background-size: cover;
        border: 4px solid #091921;
        box-shadow: 0 -15px 15px rgba(255, 255, 255, 0.05), 
        inset 0 -15px 15px rgba(255, 255, 255, 0.05), 
        0 15px 15px rgba(0, 0, 0, 0.3), 
        inset 0 15px 15px rgba(0, 0, 0, 0.3) ; /*box shadow bien integré*/
        border-radius: 50%;
    }

    .clock::before{
        content: " ";
        position: absolute;
        width: 15px;
        height: 15px;
        background-color: aliceblue;
        border-radius: 50%;
        z-index: 50;
    }


    .clock .hour{
        width: 160px;
        height: 160px;
    }

    .clock .min{
        width: 190px;
        height: 190px;
    }

    .clock .sec{
        width: 230px;
        height: 230px;
    }

    .hour, .min, .sec{
        display: flex;
        justify-content: center;
        /*align-items: center;*/
        position: absolute;
    }

    .hour::before{
        content: " ";
        position: absolute;
        width: 8px;
        height: 80px;
        background-color: crimson;
        z-index: 10 ;
        border-radius: 6px 6px 0 0;
    }

    .min::before{
        content: " ";
        position: absolute;
        width: 4px;
        height: 100px;
        background-color: whitesmoke;
        z-index: 20 ;
        border-radius: 6px 6px 0 0;
    }

    .sec::before{
        content: " ";
        position: absolute;
        width: 2px;
        height: 150px;
        background-color: whitesmoke;
        z-index: 30 ;
        border-radius: 6px 6px 0 0;
    }
</style>