<!DOCTYPE html>
<html lang="en" >
<head>
    <meta charset="UTF-8">
    <title> Parallax scroll </title>
    <meta name="viewport" content="width=device-width, initial-scale=1"><link rel="stylesheet" href="./style.css">
   
</head>
<body>
    <!-- partial:index.partial.html-->
    <svg xmlns="http://www.w3.org/2000/svg" xmnls:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 750 500" preserveAspectRatio="xMidMax slice" />
        <defs>
            <!-- Scene 1 Gradient -->
            <linearGraadient id="grad1" x1="-154.32" y1="263.27" x2="-154.32" y2="373.3"
               gradienTransform="matrix(-1, 0, 0, 1.36, 231.36, -100.14)" gradientUnits="userSpaceOnUse" >

               <stop offset="0.07" stop-color="#9c536b" />
               <stop offset="0.98" stop-color="#d98981" />
            </linearGraadient>
            <radialGradient id="bg_grad" cx="375" cy="-35" r="318.69" gradientUnits="userSpaceOnUse">
                <stop offset="0.1" stop-color="#F5C54E" id="sun"/>
                <stop offset="0.1" stop-color="#FFDBA6" />
                <stop offset="0.0" stop-color="#F7BB93" />
                <stop offset="0.0" stop-color="#F2995E" />
                <stop offset="0.0" stop-color="#F07560" />
                <stop offset="0.8" stop-color="#FFAB93" />
            </radialGradient>
            <linearGradient id="grad2" x1="242.5" y1="356.25" x2="750" y2="356.25" gradientUnits="userSpaceOnUse">
                <stop offset="0" stop-color="#fbbd93" />
                <stop offset="0.98" stop-color="#c46976" />
            </linearGradient>
<linearGradient id="grad3" x1="467.26" y1="500" x2="467.26" y2="225.47" gradientUnits="userSpaceOnUse">
                <stop offset="0.01" stop-color="#ffb8bd" />
                <stop offset="1" stop-color="#914d64" />
            </linearGradient>
            <linearGradient id="grad4" x1="216.56" y1="227.64" x2="191.14" y2="600.82" gradientUnits="userSpaceOnUse">
                <stop offset="0" stop-color="#70375a" />
                <stop offset="0.96" stop-color="#8a6e95" />
            </linearGradient>
            <linearGradient id="grad5" x1="1" y1="413.12" x2="340.58" y2="413.12" gradientUnits="userSpaceOnUse">
                <stop offset="0" stop-color="#433d6c" />
                <stop offset="1" stop-color="#392e54" />
            </linearGradient>
            <linearGradient id="grad6" x1="454.13" y1="295.96" x2="454.13" y2="498.93" gradientUnits="userSpaceOnUse">
                <stop offset="0" stop-color="#2b2850" />
                <stop offset="0.99" stop-color="#563a6a" />
            </linearGradient>
            <linearGradient id="grad7" x1="434.38" y1="391.96" x2="474.27" y2="516.33" gradientUnits="userSpaceOnUse">
                <stop offset="0.3" stop-color="#1c1b38" />
                <stop offset="0.38" stop-color="#201e3e" />
                <stop offset="0.9" stop-color="#383263" />
            </linearGradient>
            <linearGradient id="grad8" x1="259.18" y1="335.54" x2="213.65" y2="500.39" gradientUnits="userSpaceOnUse">
                <stop offset="0" stop-color="#0e0a1a" />
                <stop offset="0.3" stop-color="#100d1f" />
                <stop offset="0.64" stop-color="#17142c" />
                <stop offset="0.95" stop-color="#201f3f" />
            </linearGradient>
            <linearGradient id="grad9" x1="508.16" y1="321.39" x2="726.97" y2="623.69" gradientUnits="userSpaceOnUse">
                <stop offset="0.01" stop-color="#120e22" />
                <stop offset="1" stop-color="#221d42" />
            </linearGradient>

            <!-- Scene Gradient -->
            <linearGradient id="lg4" x1="641.98" y1="274.9" x2="638.02" y2="334.36" gradientUnits="userSpaceOnUse">
                <stop offset="0" stop-color="#2c2c50" />
                <stop offset="1" stop-color="#434375" />
            </linearGradient>
            <linearGradient id="lg5" x1="172.37" y1="286.02" x2="171.33" y2="343.08" gradientUnits="userSpaceOnUse" />
            
            <linearGradient id="lg6" x1="505.71" y1="261.55" x2="504.61" y2="322.08" gradientUnits="userSpaceOnUse" />
            
            <linearGradient id="lg7" x1="301.32" y1="260.99" x2="295.66" y2="345.9" gradientUnits="userSpaceOnUse" />

            <linearGradient id="lg8" x1="375.59" y1="381.01" x2="373.3" y2="507.08" gradientUnits="userSpaceOnUse" />

            <!-- Scene3 Gradient-->
            <radialGradient id="bg2-grad" cx="365.22" cy="500" r="631.74"
                gradientTransform="translate(750 552.6) rotate(180) scale(1 1.11)" gradientUnits="userSpaceOnUse">
                <stop offset="0" stop-color="hsla(349, 94%, 75%, 1)" />
                <stop offset="0.12" stop-color="hsla(342, 49%, 62%, 1)" />
                <stop offset="0.18" stop-color="hsla(328, 37%, 56%, 1)" />
                <stop offset="0.33" stop-color="hsla(281, 33%, 48%, 1)" />
                <stop offset="0.41" stop-color="hsla(268, 38%, 48%, 1)" />
                <stop offset="0.45" stop-color="hsla(266, 38%, 43%, 1)" />
                <stop offset="0.55" stop-color="hsla(261, 37%, 32%, 1)" />
                <stop offset="0.64" stop-color="hsla(253, 36%, 24%, 1)" />
                <stop offset="0.72" stop-color="hsla(244, 33%, 19%, 1)" />
                <stop offset="0.78" stop-color="hsla(240, 33%, 17%, 1)" />
            </radialGradient>

<div class="scrollElement"></div>

<a href="https://codepen.io/nothing4us/pens/public" target="_blank" class="btn btn_works">My Works</a>
<button class="btn" id="fullscr">Go Fullscreen</button>
<!-- Partial-->
  <script src='https//cdnjs.cloudflare.com/ajax/libs/gsap/3.3.4/gsap.min.js'></script>
  <script src='https//cdnjs.cloudflare.com/ajax/libs/gsap/3.3.4/ScrollTrigger.min.js'></script><script src="./script.js"></script>
  
</body>
</html>
