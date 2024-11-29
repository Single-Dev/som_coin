<template>
    <main>
        <div align="center">
            <a href="https://ton.org/"><img width="48" src="./assets/tapps.png" alt="logo of telegram web apps"></a>
        </div>
        <h1>Modals</h1>
        <button onclick="Telegram.WebApp.showAlert('Hello World!');">Launch Alert</button>
        <button onclick="showPopup();">Launch Popup</button>

        <h1>Links</h1>
        <ul>
            <li>
                <a href="javascript:Telegram.WebApp.openTelegramLink('https://t.me/trendingapps');">Open link within
                    Telegram</a>
            </li>
            <li>
                <a href="javascript:Telegram.WebApp.openLink('https://ton.org/');">Open link in external browser</a>
            </li>
            <li>
                <a href="javascript:Telegram.WebApp.openLink('https://telegra.ph/api',{try_instant_view:true});">Open
                    link inside Telegram webview</a>
            </li>
        </ul>

        <h1>Buttons</h1>
        <button @click="Telegram.WebApp.expand();">Expand Webview</button>
        <button @click="toggleMainButton();">Toggle Main Button</button>
    </main>
    <div id="viewport"></div>
    <div id="viewport-params-size"></div>
    <div id="viewport-params-expand"></div>
</template>
<script>
import Telegram from '@twa-dev/sdk'
export default {
    methods: {
        showPopup() {
            this.Telegram.WebApp.showPopup({
                title: 'Title',
                message: 'Some message',
                buttons: [
                    {id: 'link', type: 'default', text: 'Open ton.org'},
                    {type: 'cancel'},
                ]
            }, function(btn) {
                if (btn === 'link') {
                    this.Telegram.WebApp.openLink('https://ton.org/');
                }
            });
        },
        toggleMainButton() {
            if (this.Telegram.WebApp.MainButton.isVisible) {
                this.Telegram.WebApp.MainButton.hide();
            } else {
                this.Telegram.WebApp.MainButton.show();
            }
        },
        setViewportData() {
            var sizeEl = document.getElementById('viewport-params-size');
            sizeEl.innerText = 'width: ' + window.innerWidth + ' x ' + 
                'height: ' + this.Telegram.WebApp.viewportStableHeight;

            var expandEl = document.querySelector('#viewport-params-expand');
            expandEl.innerText = 'Is Expanded: ' + (this.Telegram.WebApp.isExpanded ? 'true' : 'false');
        }
    },
    mounted() {
        this.Telegram.WebApp.ready()
        this.Telegram.WebApp.onEvent('themeChanged', function() {
            document.documentElement.className = this.Telegram.WebApp.colorScheme;
        });
        // Show main button
        this.Telegram.WebApp.MainButton.setParams({
            text: 'Main Button'
        });
        this.Telegram.WebApp.MainButton.onClick(function () {
            this.Telegram.WebApp.showAlert('Main Button was clicked')
        });	
        this.Telegram.WebApp.MainButton.show();
        this.Telegram.WebApp.setHeaderColor('secondary_bg_color');

        this.setViewportData();
this.Telegram.WebApp.onEvent('viewportChanged', setViewportData);

this.Telegram.WebApp.onEvent('themeChanged', function() {
    document.body.setAttribute('style', '--bg-color:' + this.Telegram.WebApp.backgroundColor);
});
    },
}
</script>
<style lang="">
     body {
            --bg-color: var(--tg-theme-bg-color);
            font: 12px/18px "Lucida Grande", "Lucida Sans Unicode", Arial, Helvetica, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--tg-theme-text-color);
            margin: 48px 24px;
            padding: 0;
            color-scheme: var(--tg-color-scheme);
        }

        a {
            color: var(--tg-theme-link-color);
        }
        #viewport {
            position: fixed;
            left: 0;
            right: 0;
            top: 0;
            height: var(--tg-viewport-stable-height, 100vh);
            pointer-events: none;
            transition: all .2s ease;
        }
        #viewport:after {
            content: '';
            display: block;
            position: absolute;
            left: 0;
            right: 0;
            top: 0;
            bottom: 0;
            border-width: 4px;
            border-style: solid;
            border-image: linear-gradient(45deg, rgba(64, 224, 208, .5), rgba(173, 255, 47, .5)) 1;
        }

        #viewport-params-size,
        #viewport-params-expand {
            content: attr(text);
            position: absolute;
            display: inline-block;
            background: var(--tg-theme-link-color, rgb(64, 224, 208));
            right: 4px;
            left: auto;
            font-size: 8px;
            padding: 4px;
            vertical-align: top;
        }
        #viewport-params-size {
            top: 4px;
        }
        #viewport-params-expand {
            top: 30px;
        }
</style>