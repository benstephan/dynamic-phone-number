# Dynamic Phone Number Switching jQuery
Switch the phone number based on where traffic is coming from. The code was developed to switch whether the user was coming from a paid Google ad or an organic search lead. The 111-111-1111 number is the paid ad and the 111-111-1112 is orgabic. Each adds a cookie to the browser, but the PPC cookie always trumps the oragnic cookie for one month. 

var getUrlParameter = function getUrlParameter(sParam) {
    var sPageURL = window.location.search.substring(1),
        sURLVariables = sPageURL.split('&'),
        sParameterName,
        i;

    for (i = 0; i < sURLVariables.length; i++) {
        sParameterName = sURLVariables[i].split('=');

        if (sParameterName[0] === sParam) {
            return sParameterName[1] === undefined ? true : decodeURIComponent(sParameterName[1]);
        }
    }
};
var tech = getUrlParameter('utm_medium');
var referrer =  document.referrer;

if(tech == 'cpc'){
	$('a').each(function() {
	   var a = new RegExp('tel:1111111111');
	   if (a.test(this.href)) {
			$(this).html('<a href="tel:1111111112">111-111-1112</a>');
	   }
	});
	 var cookieName = "visitorFromAdwords"; // Name of your cookie
	 var cookieValue = "true"; // Value of your cookie
	 var expirationTime = 2592000; // One month in seconds
	 expirationTime = expirationTime * 1000; // Converts expirationtime to milliseconds
	 var date = new Date(); 
	 var dateTimeNow = date.getTime(); 

	 date.setTime(dateTimeNow + expirationTime); // Sets expiration time (Time now + one month)
	 var date = date.toUTCString(); // Converts milliseconds to UTC time string
	 document.cookie = cookieName+"="+cookieValue+"; expires="+date+"; path=/; domain=." + location.hostname.replace(/^www\./i, ""); // Sets cookie for all subdomains
	
	
}else if(referrer == 'https://www.google.com/' && tech != 'cpc'){
	console.log(referrer);
	console.log('if statement');
	
	$('a').each(function() {
	   var a = new RegExp('tel:1111111111');
	   if (a.test(this.href)) {
			$(this).html('<a href="tel:1111111111">111-111-1111</a>');
	   }
	});
	 var cookieName = "visitorFromOrganic"; // Name of your cookie
	 var cookieValue = "true"; // Value of your cookie
	 var expirationTime = 2592000; // One month in seconds
	 expirationTime = expirationTime * 1000; // Converts expirationtime to milliseconds
	 var date = new Date(); 
	 var dateTimeNow = date.getTime(); 

	 date.setTime(dateTimeNow + expirationTime); // Sets expiration time (Time now + one month)
	 var date = date.toUTCString(); // Converts milliseconds to UTC time string
	 document.cookie = cookieName+"="+cookieValue+"; expires="+date+"; path=/; domain=." + location.hostname.replace(/^www\./i, ""); // Sets cookie for all subdomains
}
function readCookie(name) {
	var nameEQ = name + "=";
	var ca = document.cookie.split(';');
	for (var i=0;i < ca.length;i++) {
		var c = ca[i];
		while (c.charAt(0)==' ')
			c = c.substring(1,c.length);
		if (c.indexOf(nameEQ) == 0)
			return c.substring(nameEQ.length,c.length);
	}
	return null;
}

