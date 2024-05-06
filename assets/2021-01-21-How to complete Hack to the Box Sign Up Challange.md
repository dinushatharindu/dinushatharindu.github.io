---
title: How to complete hack to the box sign up challange
date: 2021-01-21- 20:14 +0300
categories: [Blogging, hacking,]
tags: [blog, hacking, Growth,IT, industry]
author: Dinusha Tharindu
---

  



I think everyone knows about "hack the box" ( https://www.hackthebox.eu/). it's a cool place to learn about cybersecurity. owners made It more attractive by adding challenges to resolve. simply you have to hack the site in order to Sign up 😁 .  nice . 

  

Let see how we hack the signup page ( https://www.hackthebox.eu/invite )

  

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjqlcKRYiMKj9vNjip1D7p64TUbAw8FyEBH6IHyTjAkt6VB6LEBWUA5Gw9qwO2SM_xdjw2JoG4uOftSaPasfxYAWMgVeJS6eIjRe-edqeLAWI4XgWI_8BfdUpJP2natcyzNE2YdNecRC4U4/w563-h341/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjqlcKRYiMKj9vNjip1D7p64TUbAw8FyEBH6IHyTjAkt6VB6LEBWUA5Gw9qwO2SM_xdjw2JoG4uOftSaPasfxYAWMgVeJS6eIjRe-edqeLAWI4XgWI_8BfdUpJP2natcyzNE2YdNecRC4U4/)

  
  

    Been thank full to their Hint lets go to the Console page.  ( Right Click > Inspect )

  

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgHBULSgra-kWHZf3PHFOcOyNwWiHIH4CdiPNwCc0pdycGObaDxjfo6b3ZhfDZiwxW72DhN_hBreRt0fcZlfxK_2BLLk5xDTKKrJl4jiLGGy1Lf4xyfFho-sW8ge1u-D3CcSp5__vZ1Y8ka/w429-h275/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgHBULSgra-kWHZf3PHFOcOyNwWiHIH4CdiPNwCc0pdycGObaDxjfo6b3ZhfDZiwxW72DhN_hBreRt0fcZlfxK_2BLLk5xDTKKrJl4jiLGGy1Lf4xyfFho-sW8ge1u-D3CcSp5__vZ1Y8ka/)

  

  

If you looked for more, you can find more Hints hidden in the page source. Here's a one. 

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilsLZvqIaimNr8edYT_fvwq9XrtcG7f9wFo0fJd_Uqqcyz1n2x1Y90lWqjA5B_Y1UNL4urqOsgdJYJ-EcHoytgCL2K2FjUCBpn6dsdSqc7nCE1DN6jgv7Z9XG9uU_AqBqjUSRu18Rksjtx/w494-h337/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEilsLZvqIaimNr8edYT_fvwq9XrtcG7f9wFo0fJd_Uqqcyz1n2x1Y90lWqjA5B_Y1UNL4urqOsgdJYJ-EcHoytgCL2K2FjUCBpn6dsdSqc7nCE1DN6jgv7Z9XG9uU_AqBqjUSRu18Rksjtx/)

So the next hint is the page is loaded with Javascript so let's find where it's hidden. 

  

usually, the javascript file extension is " . JS " so now you know where to look. it seems we have a few but I'm particularly inserted in one script called " inviteapi.min.js ".

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhPs-h6lYhu3epNAvnrLFQ57z321FsdqTJl0uB90_PlRC7Ceocq-pO39U0lk4Rzm9h-g5TKQ3P2Cnx_1h9noDKDGgDeBXG60nUjbW32g1PBym5PDRIUizU3HyE_jSa6vccFe53_wzhmVj-E/w598-h217/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhPs-h6lYhu3epNAvnrLFQ57z321FsdqTJl0uB90_PlRC7Ceocq-pO39U0lk4Rzm9h-g5TKQ3P2Cnx_1h9noDKDGgDeBXG60nUjbW32g1PBym5PDRIUizU3HyE_jSa6vccFe53_wzhmVj-E/)

  

Now we have the path to the Javascript so then let's try to access it from the browser. ( it's obviously a web directory ) it's all about making the correct URL and the Path to the File.

  

So you will have something like this as the Full path. 

  

"https://www.hackthebox.eu/js/inviteapi.min.js"

  

Put it on any browser and hit enter , you'll directly go into the script.

  

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjP3DFyJ6owmRJB4MKnLFFasFgm9DK_0FOMhHm7DOoxn0NGOY5Gv-fFQUiT1AcB_dzsqCjGiyOhUogymCxDLvyiMF4nPt6SDYDKA3zP0xCujQemouL1QdS6ULZB6Q3ZtqsAFfPIPYS3QPxe/w404-h130/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjP3DFyJ6owmRJB4MKnLFFasFgm9DK_0FOMhHm7DOoxn0NGOY5Gv-fFQUiT1AcB_dzsqCjGiyOhUogymCxDLvyiMF4nPt6SDYDKA3zP0xCujQemouL1QdS6ULZB6Q3ZtqsAFfPIPYS3QPxe/)

Its looks like this so it's better if you can use a text editor like notepad++ to breakdown the script. 

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhw4iU41aHXTY7c4ZQ_JLEsw3IksciGxP5VwSY5Q0lt1I9aGzV7vLTu0Q3U2q1d3fNycooYpONM_BF5cCwZuqOmcjUjhvjkY3w9SEeydomsr7UM5oCS7qQCw2ROZLoofI5RUpHQ2dvpUkAq/w479-h231/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhw4iU41aHXTY7c4ZQ_JLEsw3IksciGxP5VwSY5Q0lt1I9aGzV7vLTu0Q3U2q1d3fNycooYpONM_BF5cCwZuqOmcjUjhvjkY3w9SEeydomsr7UM5oCS7qQCw2ROZLoofI5RUpHQ2dvpUkAq/)

  

Ok, now you have something like above, so look for the next hint. so assuming the above-highlighted text are functions I have searched that text name on the console search. 

  

  

Boom 😀. 

  

"makeInviteCode" responded with successful text so let's recall the same function with Full correct syntax

  

" makeInviteCode() "

  

Lalalala La 😀.  Ok, we have the full data set called by the function.

  

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgRCIt1CkqJMTNsL6wf5tnmX_XpM4msBzHcnojQhDjDFwu0StRQb-FSqeWKnBv4sFfC_gHAyBmu3Mehn2RP6cwUKrEjWhEqe6Wy9lRcyuBj0VBi9YTLRn8C_5iHq2EhEFp1UdgDU5jLHuRt/w631-h266/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgRCIt1CkqJMTNsL6wf5tnmX_XpM4msBzHcnojQhDjDFwu0StRQb-FSqeWKnBv4sFfC_gHAyBmu3Mehn2RP6cwUKrEjWhEqe6Wy9lRcyuBj0VBi9YTLRn8C_5iHq2EhEFp1UdgDU5jLHuRt/)

  

  

Look at the output carefully. 

  

We have a hint 😅 with encrypted data and the type of the method it encrypted.

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEio_5m8s5PoV_QsjCwhmiutGE1FYQf2lhviMf9wAPmd8r_T2Y2dfLZf97qb-IuJpFpN-vpDz496uksA2erMVt9XDTyd6cJ_RmuKLXud5MZ_6OjlaWQu_fKQjiEx-QaucINycg_do8WgCH6m/w655-h86/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEio_5m8s5PoV_QsjCwhmiutGE1FYQf2lhviMf9wAPmd8r_T2Y2dfLZf97qb-IuJpFpN-vpDz496uksA2erMVt9XDTyd6cJ_RmuKLXud5MZ_6OjlaWQu_fKQjiEx-QaucINycg_do8WgCH6m/)

  
Next is simple because we have " Google God " 😎.

  

Just simply Search " BASE64 to Text online " , and go for the first option and convert your encrypted text into Human-readable text.

  

I used " https://cryptii.com/pipes/base64-to-text " 

  

I got something like this. 

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiILY1krWQSRCo8un-IiKnvYDLMNKtEBqhyVKw0Z4gsoAUcSAOniSKJAF6gC1ylRDtdF6SSZMHRf93S0AjJhbJsRoogyLU3iV1tZKYW07Uw3paQFHvIWaRRx82Gci6Z5v7H0yyHVvKCeTut/w644-h248/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiILY1krWQSRCo8un-IiKnvYDLMNKtEBqhyVKw0Z4gsoAUcSAOniSKJAF6gC1ylRDtdF6SSZMHRf93S0AjJhbJsRoogyLU3iV1tZKYW07Uw3paQFHvIWaRRx82Gci6Z5v7H0yyHVvKCeTut/)

  
  

So the instructions are. 

  

"In order to generate the invite code, make a POST request to /api/invite/generate"

  

Ok , How we do it ? 😐😐

  

Just Google it. 

  

After a bit of research, I found that we can use the tool called "CURL".

  

"curl is a tool to transfer data from or to a server, using one of the supported protocols."

  

Look for the MAN page for more info.

  

[https://curl.se/docs/manpage.html#-x](https://curl.se/docs/manpage.html#-x)

  

so as per the instructions we need to make a post request over the HTTPS to the mentioned URL.

  

Just go to CMD and type " curl --help " so we can have a bit of a glimpse.

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEigaXIqn5r8nu84jYhp2NAe2yRHi2neLSo6wAMjrtsORd12lHTYLmNcrSQ6ZCIufCoa_O65h9vSohDTA1-EeCvSBJUUVm63DvkocNdWDk4gN9adpsosb9yX70Qq-3HDb_M932l42d9qwaoY/w549-h225/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEigaXIqn5r8nu84jYhp2NAe2yRHi2neLSo6wAMjrtsORd12lHTYLmNcrSQ6ZCIufCoa_O65h9vSohDTA1-EeCvSBJUUVm63DvkocNdWDk4gN9adpsosb9yX70Qq-3HDb_M932l42d9qwaoY/)

  
  

after searching here and there, I came up with the command to make the post request. 

  

curl -X POST  https://www.hackthebox.eu/api/invite/generate

  

Open the command prompt or any other terminal and type the command and hit enter to get the invite code to generate. 

  

Here you go 😃. we have the code but it also encoded. 

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgl_p6Swi5n2DpXX8GJK32f3_8hTdQoGhlKJunzoIKakt0w8VggtoXmKGPdVi4nxUNjwG8JrXleD6S7Rf5wcgoCEEg03Sc1zPyH-O5ecdzPQ4LQDy9rFd_POzvmzRdeKSNnfjG37WupQoa4/w645-h119/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgl_p6Swi5n2DpXX8GJK32f3_8hTdQoGhlKJunzoIKakt0w8VggtoXmKGPdVi4nxUNjwG8JrXleD6S7Rf5wcgoCEEg03Sc1zPyH-O5ecdzPQ4LQDy9rFd_POzvmzRdeKSNnfjG37WupQoa4/)

same as before go for a google search to get the text decoded. 

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6Z-DXZXF995fNjrNH3tVKGJo2djTk0IRrZAgGIBWwrKjTblPar-SqcWHv8bzVsyjQMIiW-ssPQ7Bz_jAIb7ZFOssDyB2SG6P86OqJ-0GkGp9tZXazVrbloHl4lh2Co9CHs6tnj1H-2Is7/w643-h283/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj6Z-DXZXF995fNjrNH3tVKGJo2djTk0IRrZAgGIBWwrKjTblPar-SqcWHv8bzVsyjQMIiW-ssPQ7Bz_jAIb7ZFOssDyB2SG6P86OqJ-0GkGp9tZXazVrbloHl4lh2Co9CHs6tnj1H-2Is7/)

Whoh 😍.. We have the invitation code now. use this code on the signup page to create your Hack the Box account. 

  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi76gZ_n4tasBiFqzdvZtRE9DX19MhEeX-XPXpLMY1EsUEIO55svoz8ytgnzALCbZuEu_OTaKm7P31E9bt4IVqNvtGTbBGcG33Vc1u2vmAAo4E3YmIAVLoMjWtgB0Uu-6IOv4BR9tTGCI72/w461-h350/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi76gZ_n4tasBiFqzdvZtRE9DX19MhEeX-XPXpLMY1EsUEIO55svoz8ytgnzALCbZuEu_OTaKm7P31E9bt4IVqNvtGTbBGcG33Vc1u2vmAAo4E3YmIAVLoMjWtgB0Uu-6IOv4BR9tTGCI72/)

  
  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj9VKhia8fgTduTjJ_Pz9bt25ME_WRO_nTtiTDgWFvCouPQlBAdZnmlUzgOjRJOnaaekHLzalZDzBuyUg_B3wDTZRQyysC9xSA_SbpE4XuRtSDpvg0GLh1U_zLVnBkOWpfq9BToJL4UviSr/w465-h267/image.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj9VKhia8fgTduTjJ_Pz9bt25ME_WRO_nTtiTDgWFvCouPQlBAdZnmlUzgOjRJOnaaekHLzalZDzBuyUg_B3wDTZRQyysC9xSA_SbpE4XuRtSDpvg0GLh1U_zLVnBkOWpfq9BToJL4UviSr/)

  
  

  

Happy Learning and Happy Hacking 😎
