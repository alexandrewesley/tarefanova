const receiveMessage = function (evt) {
		'use strict';
		if (evt.data === 'MM:3PCunsupported') {
			window.cookieCheck = false;
		} else if (evt.data === 'MM:3PCsupported') {
			window.cookieCheck = true;
		}
	},
	iframe = document.querySelector('[data-mm-role=thirdptycheck]');

window.addEventListener('message', receiveMessage, false);
iframe.setAttribute('src', 'https://cookiecheck.mindmup.info/start.html');
