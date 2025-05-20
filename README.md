# Ex.08 Design of Interactive Image Gallery
## Date:

## AIM:
To design a web application for an inteactive image gallery with minimum five images.

## DESIGN STEPS:

### Step 1:
Clone the github repository and create Django admin interface.

### Step 2:
Change settings.py file to allow request from all hosts.

### Step 3:
Use CSS for positioning and styling.

### Step 4:
Write JavaScript program for implementing interactivity.

### Step 5:
Validate the HTML and CSS code.

### Step 6:
Publish the website in the given URL.

## PROGRAM :
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Cartoon Photo Gallery</title>
            <style>
                body {
                    font-family: 'Poppins', sans-serif;
                    margin: 0;
                    background: linear-gradient(135deg, #1e1e2f, #2a2a3f);
                    color: #fff;
                    overflow-x: hidden;
                    animation: bgAnimation 10s infinite alternate;
                }
                @keyframes bgAnimation {
                    0% { background: linear-gradient(135deg, #1e1e2f, #2a2a3f); }
                    50% { background: linear-gradient(135deg, #3f2a70, #1e1e2f); }
                    100% { background: linear-gradient(135deg, #2a2a3f, #1e1e2f); }
                }
                h1 {
                    text-align: center;
                    margin: 20px 0;
                    font-size: 3rem;
                    letter-spacing: 2px;
                    text-transform: uppercase;
                    color: #ce0000;
                    animation: glow 2s infinite alternate;
                }
                @keyframes glow {
                    0% { text-shadow: 0 0 10px #d5d3c2, 0 0 20px #dfdccb; }
                    100% { text-shadow: 0 0 20px #bebcae, 0 0 40px #d6d1b3; }
                }
                .gallery {
                    display: grid;
                    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
                    gap: 20px;
                    padding: 20px;
                    margin: 0 auto;
                    max-width: 1200px;
                }
                .gallery-item {
                    position: relative;
                    overflow: hidden;
                    border-radius: 15px;
                    transition: transform 0.4s, box-shadow 0.4s;
                    box-shadow: 0 8px 15px rgba(0, 0, 0, 0.5);
                }
                .gallery-item img {
                    width: 100%;
                    height: 100%;
                    object-fit: cover;
                    transition: transform 0.4s;
                }
                .gallery-item:hover {
                    transform: scale(1.05);
                    box-shadow: 0 10px 20px rgba(171, 3, 162, 0.5);
                }
                .gallery-item:hover img {
                    transform: scale(1.2);
                }
                .caption {
                    position: absolute;
                    bottom: 0;
                    background: rgba(0, 0, 0, 0.6);
                    width: 100%;
                    text-align: center;
                    padding: 12px 0;
                    font-size: 1.2rem;
                    text-transform: capitalize;
                    color: #fff;
                    transition: all 0.4s ease-in-out;
                }
                .gallery-item:hover .caption {
                    background: rgba(212, 23, 171, 0.8);
                }
                #lightbox {
                    display: none;
                    position: fixed;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    background: rgba(0, 0, 0, 0.9);
                    align-items: center;
                    justify-content: center;
                    z-index: 1000;
                    animation: fadeIn 0.5s forwards;
                }
                @keyframes fadeIn {
                    from { opacity: 0; }
                    to { opacity: 1; }
                }
                @keyframes fadeOut {
                    from { opacity: 1; }
                    to { opacity: 0; }
                }
                #lightbox img {
                    max-width: 90%;
                    max-height: 90%;
                    border: 4px solid #be199d;
                    border-radius: 12px;
                    animation: zoomIn 0.3s forwards;
                }
                @keyframes zoomIn {
                    from { transform: scale(0.8); }cd pra
                    to { transform: scale(1); }
                }
                #lightbox span {
                    position: absolute;
                    top: 20px;
                    right: 30px;
                    font-size: 2rem;
                    color: #fff;
                    cursor: pointer;
                    transition: color 0.3s;
                }
                #lightbox span:hover {
                    color: #ab137a;
                }
            </style>
        </head>
        <body>
            <h1>REDCARS-GALLARY</h1>
            <div class="gallery" id="gallery">
                <!-- Celebrity Images -->
                <div class="gallery-item">
                    <img src="car1.jpg" alt="BT21">
                    <div class="caption">FERRARI-BLUE</div>
                </div>
                <div class="gallery-item">
                    <img src="car2.jpg" alt="DOREMON">
                    <div class="caption">FERRARI-RED</div>
                </div>
                <div class="gallery-item">
                    <img src="car3.jpg" alt="POKEMON">
                    <div class="caption">FERRARI-BLACK</div>
                </div>
                <div class="gallery-item">
                    <img src="car4.jpg" alt="SHINCHAN">
                    <div class="caption">FERRARI-BERRY</div>
                </div>
                <div class="gallery-item">
                    <img src="car5.jpg" alt="SHINZO">
                    <div class="caption">FERRARI-GHOST</div>
                </div>
                <div class="gallery-item">
                    <img src="car6.jpg" alt="tom and jerry">
                    <div class="caption">FERRARI-SILVER</div>
                </div>
                <div class="gallery-item">
                    <img src="car7.jpg" alt="NR BEAN">
                    <div class="caption">FERRARI-XUV</div>
                </div>
                <div class="gallery-item">
                    <img src="car8.jpg" alt="CHOTA BEAM">
                    <div class="caption">FERRARI-PHANTOM</div>
                </div>
            </div>
            
            <div id="lightbox">
                <span id="closeLightbox">&times;</span>
                <img src="" alt="Large Image" id="lightboxImg">
            </div>
        
            <script>
                const galleryItems = document.querySelectorAll('.gallery-item img');
                const lightbox = document.getElementById('lightbox');
                const lightboxImg = document.getElementById('lightboxImg');
                const closeLightbox = document.getElementById('closeLightbox');
                let currentIndex = 0;
        
                function openLightbox(index) {
                    currentIndex = index;
                    lightboxImg.src = galleryItems[index].src;
                    lightbox.style.display = 'flex';
                }
        
                function close() {
                    lightbox.style.display = 'none';
                }
        
                galleryItems.forEach((img, index) => {
                    img.addEventListener('click', () => openLightbox(index));
                });
        
                closeLightbox.addEventListener('click', close);
            </script>
            <footer align="center" id="copywrite">
                Designed and developed by BERRY & CO-CARS 
            </footer>
        </body>
        </html>
## OUTPUT:

![image](https://github.com/user-attachments/assets/54baf62b-ca44-460d-a694-fb141f4a0c32)


## RESULT:
The program for designing an interactive image gallery using HTML, CSS and JavaScript is executed successfully.
