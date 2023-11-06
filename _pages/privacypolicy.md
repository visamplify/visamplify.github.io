(function() { window.twoseven = window.twoseven || {}; })();(function() { window.twoseven.waitForDOMNode = async function t(e,t=document){e=e||{};const{type:n,value:o}=e;if(!n||!o)throw new Error("Must specify identifier");let s=o;switch(n){case"tag":s=o.toUpperCase()}if("check"!==n){const e=i({type:"selector",value:s},\[\],t);if(e)return new Promise(t=>t(e))}function i({type:e,value:t},n,o){let s;switch(e){case"tag":s=n.find(e=>e.tagName===t);break;case"selector":s=o.querySelector(t)}return s}async function a({type:e,value:t},n,o){let s;switch(e){case"tag":s=n.find(e=>e.tagName===t);break;case"selector":s=o.querySelector(t);break;case"check":for(const e of n){if(await t(e))return e}}return s}return new Promise((e,o)=>{const r=new MutationObserver(async o=>{for(const w of o)if("childList"===w.type){const o=Array.from(w.addedNodes);let d;if(d="check"===n?await a({type:n,value:s},o,t):await i({type:n,value:s},o,t))return r.disconnect(),e(d)}});r.observe(t,{childList:!0,subtree:!0})})}; })();(function() { window.twoseven.reportError = function n(e,t,n){"string"==typeof(n=n||{})&&(n={message:n});const{message:o,stack:s}=t;Object.assign(n,{tag:e,error:{message:o,stack:s}}),window.tsExtGetPostToParent()({name:name,tag:e,action:"report-error",json:n}),console.error(JSON.stringify(n.error))} ; })();(function() { window.twosevenHmsToSecondsOnly = function(str) { var p = str.split(':'), s = 0, m = 1; while (p.length > 0) { s += m \* parseInt(p.pop(), 10); m \*= 60; } return s; } ; })();(function() { window.twosevenExtLog = function(e,o,c){o||(o=e,e=void 0);let n=c||"black";if(c)switch(c){case"success":n="Green";break;case"info":n="DodgerBlue";break;case"error":n="Red";break;case"warning":n="Orange";break;default:n=c}e?console.log("%c"+e+": "+o,\`color:${n}\`):console.log("%c"+o,\`color:${n}\`)}; })();(function() { document.twosevenGET = function(url, callback) { var xmlhttp = new XMLHttpRequest(); xmlhttp.onreadystatechange = function() { if (xmlhttp.readyState == XMLHttpRequest.DONE ) { if (xmlhttp.status == 200) { callback(null, xmlhttp.responseText); } else { callback('something else other than 200 was returned', ''); } } }; xmlhttp.open("GET", url, true); xmlhttp.send(); }; ; })();(function() { window.triggerEvent = function(e,t,n,o=!1){let s;o?(n&&"string"!=typeof n&&(n=JSON.stringify(n)),s=n):s={data:n},window.twosevenScriptsDiv&&n&&"object"==typeof n&&(console.warn(\`WARNING: Attempting to send an object via event.detail from CS->Page does not work on Firefox: ${JSON.stringify(n)}\`),console.error((new Error).stack));const i=new CustomEvent(t,{bubbles:!0,composed:!0,detail:s});e.dispatchEvent(i)} ; })();(function() { window.twoseven.postTo = async function o(e,t,n=!1){let o;return t.name=t.name||name,o=n?new Promise(e=>{const n=\`ack-${t.action}-${1e9\*Math.random()|0}\`;t.ack={event:n};window.debug&&\["play","pause","currentTime"\].some(e=>t.action.includes(e)),window.addEventListener("message",function t({data:o={}}){o.action===n&&(window.removeEventListener("message",t),e(o.json))})}):new Promise(e=>e()),e.postMessage(t,"\*"),o}; })();(function() { window.tsExtGetPostTo = function s(){return window.twoseven&&window.twoseven.postTo||window.postTo}; })();(function() { window.tsExtGetPostToParent = function i(){return window.twoseven&&window.twoseven.postToParent||window.postToParent}; })();(function() { window.twoseven.postResponse = async function a(e,t){const{source:n,data:{ack:{event:o}}}=e;window.tsExtGetPostTo()(n,{action:o,json:t})}; })();(function() { window.postResponse = async function a(e,t){const{source:n,data:{ack:{event:o}}}=e;window.tsExtGetPostTo()(n,{action:o,json:t})}; })();(function() { window.twoseven.postToParent = async function r(e,t=!1){return window.tsExtGetPostTo()(window.parent,e,t)}; })();(function() { window.twoseven.postToTop = async function w(e,t=!1){return window.tsExtGetPostTo()(window.top,e,t)}; })();(function() { window.postToTop = async function w(e,t=!1){return window.tsExtGetPostTo()(window.top,e,t)}; })();(function() { window.twoseven.getFromStorage = e=>new Promise((t,n)=>{const o="get-from-storage-"+(1e9\*Math.random()|0);window.addEventListener(o,e=>{window.removeEventListener(o,this);const{detail:{data:{value:n}}}=e;t(n)}),triggerEvent(window,"get-from-storage",{key:e,evt:o})}) window.twoseven.saveToStorage = e=>{triggerEvent(window,"save-to-storage",e)} ; })();(function() { window.attachHistoryListeners = function d(){const e=history.pushState;history.pushState=function(t,n,o){return"function"==typeof history.onpushstate&&history.onpushstate({state:t}),triggerEvent(window,"pushstate",{uri:o}),e.apply(history,arguments)};const t=history.replaceState;history.replaceState=function(e){return"function"==typeof history.onreplacestate&&history.onreplacestate({state:e}),t.apply(history,arguments)}} window.attachHistoryListeners() ; })();(function() { window.twoseven.once = function c(e,t,n){e.addEventListener(t,function o(s){e.removeEventListener(t,o),n(s)})}; })();(function() { window.nextTick = function v(){return new Promise(e=>setTimeout(e,0))}; })();(function() { window.twoseven.isOnTwoSevenTab = async () => { const result = await window.twoseven.postTo(window, { action: 'is-on-twoseven-tab' }, true) return result } ; })();(function() { window.twoseven.isPaused = async () => { const result = await window.twoseven.postTo(window, { action: 'twoseven:pause-state' }, true) return result } ; })();(function() { window.twoseven.waitForProp = function u(e,t,n){return new Promise(o=>{if(e\[t\])return void o();const s=setInterval(()=>{e\[t\]&&(clearInterval(s),o())},n)})}; })();(function() { window.twoseven.overrideMethod = function p(e,t,n){const o=e\[t\].bind(e);e\[t\]=async function(...e){return await n(...e),o(...e)}}; })();(function() { window.twoseven.waitForVideoTimeUpdate = function g(e,t=3){return new Promise(n=>{let o=0;const s=()=>{++o===t&&(e.removeEventListener("timeupdate",s),n())};e.addEventListener("timeupdate",s)})}; })();(function() { window.twoseven.waitForVideoReadyState = function l(e,t,n=30){return t(e.readyState)?Promise.resolve():new Promise(o=>{const s=setInterval(()=>{t(e.readyState)&&(clearInterval(s),o())},n)})}; })();(function() { window.twoseven.waitForVideoToHaveFutureData = function m(e,...t){return window.twoseven.waitForVideoReadyState(e,e=>e>=3,...t)}; })();(function() { window.twoseven.waitForSameSiteCookies = function f(){return window.twoseven.waitForProp(window.twoseven,"\_\_cookiesUpdated")}; })();(function() { window.twoseven = window.twoseven || {}; })();(function() { window.twoseven.waitForDOMNode = async function t(e,t=document){e=e||{};const{type:n,value:o}=e;if(!n||!o)throw new Error("Must specify identifier");let s=o;switch(n){case"tag":s=o.toUpperCase()}if("check"!==n){const e=i({type:"selector",value:s},\[\],t);if(e)return new Promise(t=>t(e))}function i({type:e,value:t},n,o){let s;switch(e){case"tag":s=n.find(e=>e.tagName===t);break;case"selector":s=o.querySelector(t)}return s}async function a({type:e,value:t},n,o){let s;switch(e){case"tag":s=n.find(e=>e.tagName===t);break;case"selector":s=o.querySelector(t);break;case"check":for(const e of n){if(await t(e))return e}}return s}return new Promise((e,o)=>{const r=new MutationObserver(async o=>{for(const w of o)if("childList"===w.type){const o=Array.from(w.addedNodes);let d;if(d="check"===n?await a({type:n,value:s},o,t):await i({type:n,value:s},o,t))return r.disconnect(),e(d)}});r.observe(t,{childList:!0,subtree:!0})})}; })();(function() { window.twoseven.reportError = function n(e,t,n){"string"==typeof(n=n||{})&&(n={message:n});const{message:o,stack:s}=t;Object.assign(n,{tag:e,error:{message:o,stack:s}}),window.tsExtGetPostToParent()({name:name,tag:e,action:"report-error",json:n}),console.error(JSON.stringify(n.error))} ; })();(function() { window.twosevenHmsToSecondsOnly = function(str) { var p = str.split(':'), s = 0, m = 1; while (p.length > 0) { s += m \* parseInt(p.pop(), 10); m \*= 60; } return s; } ; })();(function() { window.twosevenExtLog = function(e,o,c){o||(o=e,e=void 0);let n=c||"black";if(c)switch(c){case"success":n="Green";break;case"info":n="DodgerBlue";break;case"error":n="Red";break;case"warning":n="Orange";break;default:n=c}e?console.log("%c"+e+": "+o,\`color:${n}\`):console.log("%c"+o,\`color:${n}\`)}; })();(function() { document.twosevenGET = function(url, callback) { var xmlhttp = new XMLHttpRequest(); xmlhttp.onreadystatechange = function() { if (xmlhttp.readyState == XMLHttpRequest.DONE ) { if (xmlhttp.status == 200) { callback(null, xmlhttp.responseText); } else { callback('something else other than 200 was returned', ''); } } }; xmlhttp.open("GET", url, true); xmlhttp.send(); }; ; })();(function() { window.triggerEvent = function(e,t,n,o=!1){let s;o?(n&&"string"!=typeof n&&(n=JSON.stringify(n)),s=n):s={data:n},window.twosevenScriptsDiv&&n&&"object"==typeof n&&(console.warn(\`WARNING: Attempting to send an object via event.detail from CS->Page does not work on Firefox: ${JSON.stringify(n)}\`),console.error((new Error).stack));const i=new CustomEvent(t,{bubbles:!0,composed:!0,detail:s});e.dispatchEvent(i)} ; })();(function() { window.twoseven.postTo = async function o(e,t,n=!1){let o;return t.name=t.name||name,o=n?new Promise(e=>{const n=\`ack-${t.action}-${1e9\*Math.random()|0}\`;t.ack={event:n};window.debug&&\["play","pause","currentTime"\].some(e=>t.action.includes(e)),window.addEventListener("message",function t({data:o={}}){o.action===n&&(window.removeEventListener("message",t),e(o.json))})}):new Promise(e=>e()),e.postMessage(t,"\*"),o}; })();(function() { window.tsExtGetPostTo = function s(){return window.twoseven&&window.twoseven.postTo||window.postTo}; })();(function() { window.tsExtGetPostToParent = function i(){return window.twoseven&&window.twoseven.postToParent||window.postToParent}; })();(function() { window.twoseven.postResponse = async function a(e,t){const{source:n,data:{ack:{event:o}}}=e;window.tsExtGetPostTo()(n,{action:o,json:t})}; })();(function() { window.postResponse = async function a(e,t){const{source:n,data:{ack:{event:o}}}=e;window.tsExtGetPostTo()(n,{action:o,json:t})}; })();(function() { window.twoseven.postToParent = async function r(e,t=!1){return window.tsExtGetPostTo()(window.parent,e,t)}; })();(function() { window.twoseven.postToTop = async function w(e,t=!1){return window.tsExtGetPostTo()(window.top,e,t)}; })();(function() { window.postToTop = async function w(e,t=!1){return window.tsExtGetPostTo()(window.top,e,t)}; })();(function() { window.twoseven.getFromStorage = e=>new Promise((t,n)=>{const o="get-from-storage-"+(1e9\*Math.random()|0);window.addEventListener(o,e=>{window.removeEventListener(o,this);const{detail:{data:{value:n}}}=e;t(n)}),triggerEvent(window,"get-from-storage",{key:e,evt:o})}) window.twoseven.saveToStorage = e=>{triggerEvent(window,"save-to-storage",e)} ; })();(function() { window.attachHistoryListeners = function d(){const e=history.pushState;history.pushState=function(t,n,o){return"function"==typeof history.onpushstate&&history.onpushstate({state:t}),triggerEvent(window,"pushstate",{uri:o}),e.apply(history,arguments)};const t=history.replaceState;history.replaceState=function(e){return"function"==typeof history.onreplacestate&&history.onreplacestate({state:e}),t.apply(history,arguments)}} window.attachHistoryListeners() ; })();(function() { window.twoseven.once = function c(e,t,n){e.addEventListener(t,function o(s){e.removeEventListener(t,o),n(s)})}; })();(function() { window.nextTick = function v(){return new Promise(e=>setTimeout(e,0))}; })();(function() { window.twoseven.isOnTwoSevenTab = async () => { const result = await window.twoseven.postTo(window, { action: 'is-on-twoseven-tab' }, true) return result } ; })();(function() { window.twoseven.isPaused = async () => { const result = await window.twoseven.postTo(window, { action: 'twoseven:pause-state' }, true) return result } ; })();(function() { window.twoseven.waitForProp = function u(e,t,n){return new Promise(o=>{if(e\[t\])return void o();const s=setInterval(()=>{e\[t\]&&(clearInterval(s),o())},n)})}; })();(function() { window.twoseven.overrideMethod = function p(e,t,n){const o=e\[t\].bind(e);e\[t\]=async function(...e){return await n(...e),o(...e)}}; })();(function() { window.twoseven.waitForVideoTimeUpdate = function g(e,t=3){return new Promise(n=>{let o=0;const s=()=>{++o===t&&(e.removeEventListener("timeupdate",s),n())};e.addEventListener("timeupdate",s)})}; })();(function() { window.twoseven.waitForVideoReadyState = function l(e,t,n=30){return t(e.readyState)?Promise.resolve():new Promise(o=>{const s=setInterval(()=>{t(e.readyState)&&(clearInterval(s),o())},n)})}; })();(function() { window.twoseven.waitForVideoToHaveFutureData = function m(e,...t){return window.twoseven.waitForVideoReadyState(e,e=>e>=3,...t)}; })();(function() { window.twoseven.waitForSameSiteCookies = function f(){return window.twoseven.waitForProp(window.twoseven,"\_\_cookiesUpdated")}; })();(function() { const modal = document.querySelector('.twoseven-ext-tab-media-modal') const modalCloseBtn = modal.querySelector('.close') function closeModal () { modal.style.display = 'none' const frame = document.querySelector('#twoseven-ext-tab-media-iframe').contentWindow frame.postMessage({ \_\_evt\_name: 'modal-hide' }, '\*') } modalCloseBtn.onclick = closeModal window.onmessage = function (e) { if (e.data.\_\_evt\_name === 'modal-hide') { closeModal() } } window.twoseven.closeTabMediaModal = closeModal window.onclick = function (e) { if (e.target.id === 'twoseven-ext-tab-media-modal' && modal.style.display === 'block') { closeModal() } } ; })();

Terms and Conditions for Visamplify - PrivacyPolicies.com             window.dataLayer = window.dataLayer || \[\]; function gtag(){dataLayer.push(arguments);} gtag('js', new Date()); gtag('config', 'G-9D331S5YCM'); 

Terms and Conditions for Visamplify

Terms and Conditions
====================

Last updated: January 23, 2023

Please read these terms and conditions carefully before using Our Service.

Interpretation and Definitions
==============================

Interpretation
--------------

The words of which the initial letter is capitalized have meanings defined under the following conditions. The following definitions shall have the same meaning regardless of whether they appear in singular or in plural.

Definitions
-----------

For the purposes of these Terms and Conditions:

*   **Application** means the software program provided by the Company downloaded by You on any electronic device, named Visamplify
    
*   **Application Store** means the digital distribution service operated and developed by Apple Inc. (Apple App Store) or Google Inc. (Google Play Store) in which the Application has been downloaded.
    
*   **Affiliate** means an entity that controls, is controlled by or is under common control with a party, where "control" means ownership of 50% or more of the shares, equity interest or other securities entitled to vote for election of directors or other managing authority.
    
*   **Country** refers to: Ontario, Canada
    
*   **Company** (referred to as either "the Company", "We", "Us" or "Our" in this Agreement) refers to Visamplify.
    
*   **Device** means any device that can access the Service such as a computer, a cellphone or a digital tablet.
    
*   **Service** refers to the Application.
    
*   **Terms and Conditions** (also referred as "Terms") mean these Terms and Conditions that form the entire agreement between You and the Company regarding the use of the Service. This Terms and Conditions agreement has been created with the help of the [Terms and Conditions Generator](https://www.privacypolicies.com/terms-conditions-generator/).
    
*   **Third-party Social Media Service** means any services or content (including data, information, products or services) provided by a third-party that may be displayed, included or made available by the Service.
    
*   **You** means the individual accessing or using the Service, or the company, or other legal entity on behalf of which such individual is accessing or using the Service, as applicable.
    

Acknowledgment
==============

These are the Terms and Conditions governing the use of this Service and the agreement that operates between You and the Company. These Terms and Conditions set out the rights and obligations of all users regarding the use of the Service.

Your access to and use of the Service is conditioned on Your acceptance of and compliance with these Terms and Conditions. These Terms and Conditions apply to all visitors, users and others who access or use the Service.

By accessing or using the Service You agree to be bound by these Terms and Conditions. If You disagree with any part of these Terms and Conditions then You may not access the Service.

You represent that you are over the age of 18. The Company does not permit those under 18 to use the Service.

Your access to and use of the Service is also conditioned on Your acceptance of and compliance with the Privacy Policy of the Company. Our Privacy Policy describes Our policies and procedures on the collection, use and disclosure of Your personal information when You use the Application or the Website and tells You about Your privacy rights and how the law protects You. Please read Our Privacy Policy carefully before using Our Service.

Links to Other Websites
=======================

Our Service may contain links to third-party web sites or services that are not owned or controlled by the Company.

The Company has no control over, and assumes no responsibility for, the content, privacy policies, or practices of any third party web sites or services. You further acknowledge and agree that the Company shall not be responsible or liable, directly or indirectly, for any damage or loss caused or alleged to be caused by or in connection with the use of or reliance on any such content, goods or services available on or through any such web sites or services.

We strongly advise You to read the terms and conditions and privacy policies of any third-party web sites or services that You visit.

Termination
===========

We may terminate or suspend Your access immediately, without prior notice or liability, for any reason whatsoever, including without limitation if You breach these Terms and Conditions.

Upon termination, Your right to use the Service will cease immediately.

Limitation of Liability
=======================

Notwithstanding any damages that You might incur, the entire liability of the Company and any of its suppliers under any provision of this Terms and Your exclusive remedy for all of the foregoing shall be limited to the amount actually paid by You through the Service or 100 USD if You haven't purchased anything through the Service.

To the maximum extent permitted by applicable law, in no event shall the Company or its suppliers be liable for any special, incidental, indirect, or consequential damages whatsoever (including, but not limited to, damages for loss of profits, loss of data or other information, for business interruption, for personal injury, loss of privacy arising out of or in any way related to the use of or inability to use the Service, third-party software and/or third-party hardware used with the Service, or otherwise in connection with any provision of this Terms), even if the Company or any supplier has been advised of the possibility of such damages and even if the remedy fails of its essential purpose.

Some states do not allow the exclusion of implied warranties or limitation of liability for incidental or consequential damages, which means that some of the above limitations may not apply. In these states, each party's liability will be limited to the greatest extent permitted by law.

"AS IS" and "AS AVAILABLE" Disclaimer
=====================================

The Service is provided to You "AS IS" and "AS AVAILABLE" and with all faults and defects without warranty of any kind. To the maximum extent permitted under applicable law, the Company, on its own behalf and on behalf of its Affiliates and its and their respective licensors and service providers, expressly disclaims all warranties, whether express, implied, statutory or otherwise, with respect to the Service, including all implied warranties of merchantability, fitness for a particular purpose, title and non-infringement, and warranties that may arise out of course of dealing, course of performance, usage or trade practice. Without limitation to the foregoing, the Company provides no warranty or undertaking, and makes no representation of any kind that the Service will meet Your requirements, achieve any intended results, be compatible or work with any other software, applications, systems or services, operate without interruption, meet any performance or reliability standards or be error free or that any errors or defects can or will be corrected.

Without limiting the foregoing, neither the Company nor any of the company's provider makes any representation or warranty of any kind, express or implied: (i) as to the operation or availability of the Service, or the information, content, and materials or products included thereon; (ii) that the Service will be uninterrupted or error-free; (iii) as to the accuracy, reliability, or currency of any information or content provided through the Service; or (iv) that the Service, its servers, the content, or e-mails sent from or on behalf of the Company are free of viruses, scripts, trojan horses, worms, malware, timebombs or other harmful components.

Some jurisdictions do not allow the exclusion of certain types of warranties or limitations on applicable statutory rights of a consumer, so some or all of the above exclusions and limitations may not apply to You. But in such a case the exclusions and limitations set forth in this section shall be applied to the greatest extent enforceable under applicable law.

Governing Law
=============

The laws of the Country, excluding its conflicts of law rules, shall govern this Terms and Your use of the Service. Your use of the Application may also be subject to other local, state, national, or international laws.

Disputes Resolution
===================

If You have any concern or dispute about the Service, You agree to first try to resolve the dispute informally by contacting the Company.

For European Union (EU) Users
=============================

If You are a European Union consumer, you will benefit from any mandatory provisions of the law of the country in which you are resident in.

United States Legal Compliance
==============================

You represent and warrant that (i) You are not located in a country that is subject to the United States government embargo, or that has been designated by the United States government as a "terrorist supporting" country, and (ii) You are not listed on any United States government list of prohibited or restricted parties.

Severability and Waiver
=======================

Severability
------------

If any provision of these Terms is held to be unenforceable or invalid, such provision will be changed and interpreted to accomplish the objectives of such provision to the greatest extent possible under applicable law and the remaining provisions will continue in full force and effect.

Waiver
------

Except as provided herein, the failure to exercise a right or to require performance of an obligation under these Terms shall not effect a party's ability to exercise such right or require such performance at any time thereafter nor shall the waiver of a breach constitute a waiver of any subsequent breach.

Translation Interpretation
==========================

These Terms and Conditions may have been translated if We have made them available to You on our Service. You agree that the original English text shall prevail in the case of a dispute.

Changes to These Terms and Conditions
=====================================

We reserve the right, at Our sole discretion, to modify or replace these Terms at any time. If a revision is material We will make reasonable efforts to provide at least 30 days' notice prior to any new terms taking effect. What constitutes a material change will be determined at Our sole discretion.

By continuing to access or use Our Service after those revisions become effective, You agree to be bound by the revised terms. If You do not agree to the new terms, in whole or in part, please stop using the website and the Service.

Contact Us
==========

If you have any questions about these Terms and Conditions, You can contact us:

*   By email: visamplify@gmail.com

Generated using [Privacy Policies Generator](https://www.privacypolicies.com/privacy-policy-generator/)

const tabLinks = Array.from(document.querySelectorAll(".tab-link")); const tabContents = document.querySelectorAll(".tab-content"); tabLinks.forEach(function(tabLink) { tabLink.addEventListener("click", toggleTab); }); let priorActiveTab = null; function toggleTab(event) { tabLinks.forEach(function(tabLink, index){ tabLink.classList.remove("active"); tabLink.classList.add("inactive"); tabContents\[index\].classList.remove("visible"); tabContents\[index\].classList.add("hidden"); }); if(priorActiveTab === this) { this.classList.remove("active"); this.classList.add("inactive"); tabContents\[tabLinks.indexOf(this)\].classList.remove("visible"); tabContents\[tabLinks.indexOf(this)\].classList.add("hidden"); priorActiveTab = null; } else { this.classList.remove("inactive"); this.classList.add("active"); tabContents\[tabLinks.indexOf(this)\].classList.remove("hidden"); tabContents\[tabLinks.indexOf(this)\].classList.add("visible"); priorActiveTab = this; } if (priorActiveTab === null) { this.classList.remove("inactive"); this.classList.add("active"); tabContents\[tabLinks.indexOf(this)\].classList.remove("hidden"); tabContents\[tabLinks.indexOf(this)\].classList.add("visible"); } event.preventDefault(); } "use strict"; window.LCG\_TRACKING\_APPLICATION = "privacypolicies-livelink"; window.LCG\_TRACKING\_ENVIRONMENT = "production"; window.LCG\_TRACKING\_EPOCH = "2020-e01"; ![](/track/v1/px)

×
