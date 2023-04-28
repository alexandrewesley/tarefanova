/* eslint-disable */
var isIe = function () {
		'use strict';
		var userAgent = window.navigator && window.navigator.userAgent;
		return /MSIE /.test(userAgent) || /Trident\//.test(userAgent) || /Edge\//.test(userAgent);
	},
	isOldBrowser = function (err) {
		'use strict';
		var message = err && (err.message || err);
		if (message && typeof message === 'string') {
			return /Unexpected keyword 'const'/.test(message) || /let is a reserved identifier/.test(message);
		}
		return false;
	},
	sendXHRRequest = function (endpoint, content) {
		var oReq = new XMLHttpRequest();
		oReq.open('POST', endpoint);
		oReq.setRequestHeader('Content-Type', 'application/json');
		oReq.send(JSON.stringify(content));
	};
	storeError = function (err) {
		'use strict';
		try {
			if (window && window.localStorage  && window.localStorage.setItem && typeof window.localStorage.setItem === 'function') {
				var stack = err && err.stack,
					toLog = 'err:[' + String(err)  + '] stack:[' + String(stack) + ']';
				window.localStorage.setItem('page-init-error', toLog);
			}
		} catch (e) {
			console.log(e);
		}
	},
	onScriptLoadFailure = function (err) {
		'use strict';
		var title = '',
			message = '';
		storeError(err);
		if (isIe() || isOldBrowser(err)) {
			title = 'Unable to start MindMup';
			message =  'MindMup is not compatible with your browser. Please use the latest version of Chrome, Firefox or Safari.';
			window.scriptsLoadingFailedActions.setAttribute('class', 'hidden');
		} else {
			title = 'Unable to start the MindMup application';
			message =  'This might be a temporary error, or MindMup may not be compatible with your browser. Please use the latest version of Chrome, Firefox or Safari.';
		}
		if (title && window.fatalErrorTitle) {
			window.fatalErrorTitle.innerHTML = title;
		}
		if (message && window.fatalErrorMessage) {
			window.fatalErrorMessage.innerHTML = message;
		}
		if (window.scriptsLoading) {
			window.scriptsLoading.classList.add('hidden');
		}
		if (window.scriptsLoadingFailed) {
			window.scriptsLoadingFailed.classList.remove('hidden');
		}
	};

window.addEventListener('load', function () {
	'use strict';
	if (isIe()) {
		return onScriptLoadFailure('unsupported-browser');
	}
	var initPage = function () {
		try {
			mmStart();
		} catch (e) {
			window.console.log(e);
			onScriptLoadFailure(e);
		}
	};
	if (document.fonts && document.fonts.ready) {
		document.fonts.ready.then(initPage);
	} else {
		initPage();
	}
});
