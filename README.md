# BeutaBanners
 - Beutiful banners for static websites!
---
## How to implement-
 - HTML Implementation:
```HTML
<!DOCTYPE html>
<html lang="en-US">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E4ST</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@24,400,0,0&icon_names=info" />
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="banner" id="banner1">
        <span class="material-symbols-outlined">info</span>
        <h4>Want to visit the old version?</h4>
        <p>
            Click <a href="<!-- Put your destination link here-->">here</a> to go there!
        </p>
        <button onclick="dismissBanner('banner1')">Dismiss</button>
    </div>
    <div class="banner" id="banner2">
        <span class="material-symbols-outlined">info</span>
        <h4>Wrong page?</h4>
        <p>
            Click <a href="<!-- Put your destination link here-->">here</a> to see why.
        </p>
        <button onclick="dismissBanner('banner2')">Dismiss</button>
    </div>
    <footer>
        <p>Coded on XX/XX/20XX (XX/XX/20XX for U.S.A.)</p>
        <button onclick="restoreBanners()">Restore Banners</button>
    </footer>

    <script src="./scripts.js"></script>
</body>
</html>
```
 - CSS Implementation:
```CSS
/* Preset CSS with required classes! */
.banner {
    position: fixed;
    left: 10px;
    right: 10px;
    background: #f9f9f9;
    border: 1px solid #ccc;
    padding: 10px;
    border-radius: 5px;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
    opacity: 1;
    transition: opacity 0.3s ease-in-out, bottom 0.3s ease-in-out;
}

.banner.show {
    opacity: 1;
}

.banner.hide {
    opacity: 0;
    pointer-events: none;
}
```
 - JavaScript Implementation:
```JavaScript
document.addEventListener('DOMContentLoaded', () => {
    const banners = document.querySelectorAll('.banner');
    let bannerBottomPosition = 10;

    banners.forEach(banner => {
        const bannerId = banner.id;

        if (localStorage.getItem(bannerId) === 'dismissed') {
            banner.style.display = 'none';
        } else {
            banner.style.display = 'block';
            banner.classList.add('show');
            banner.style.bottom = `${bannerBottomPosition}px`;
            bannerBottomPosition += banner.offsetHeight + 10;
        }
    });
});

function dismissBanner(bannerId) {
    const banner = document.getElementById(bannerId);

    if (banner) {
        banner.classList.remove('show');
        banner.classList.add('hide');
        banner.addEventListener(
            'transitionend',
            () => {
                banner.style.display = 'none';
                localStorage.setItem(bannerId, 'dismissed');
                adjustBannerPositions();
            },
            { once: true }
        );
    }
}

function restoreBanners() {
    const banners = document.querySelectorAll('.banner');
    let bannerBottomPosition = 10;

    banners.forEach(banner => {
        localStorage.removeItem(banner.id);
        banner.style.display = 'block';
        banner.classList.remove('hide');
        banner.classList.add('show');
        banner.style.bottom = `${bannerBottomPosition}px`;
        bannerBottomPosition += banner.offsetHeight + 10;
    });
}

function adjustBannerPositions() {
    const banners = document.querySelectorAll('.banner');
    let bannerBottomPosition = 10;

    banners.forEach(banner => {
        if (banner.style.display !== 'none') {
            banner.style.bottom = `${bannerBottomPosition}px`;
            bannerBottomPosition += banner.offsetHeight + 10;
        }
    });
}
```
---
## How do I use it?

Just copy and paste the code into the pages you want the banners to appear in, and customise to fit the theme!
---
## PLEASE ATTRIBUTE!
