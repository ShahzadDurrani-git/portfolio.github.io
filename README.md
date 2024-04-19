
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Coming Soon</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div id="magic"></div>
    <div class="playground"></div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="functions.js"></script>
    <script type="x-shader/x-vertex" id="vertexshader">

      attribute float size;
      attribute vec3 customColor;
      varying vec3 vColor;

      void main() {

        vColor = customColor;
        vec4 mvPosition = modelViewMatrix * vec4( position, 1.0 );
        gl_PointSize = size * ( 300.0 / -mvPosition.z );
        gl_Position = projectionMatrix * mvPosition;

      }
    </script>
    <script type="x-shader/x-fragment" id="fragmentshader">

      uniform vec3 color;
      uniform sampler2D pointTexture;

      varying vec3 vColor;

      void main() {

        gl_FragColor = vec4( color * vColor, 1.0 );
        gl_FragColor = gl_FragColor * texture2D( pointTexture, gl_PointCoord );

      }
    </script>
  </body>
</html>
