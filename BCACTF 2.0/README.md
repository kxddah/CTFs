<h2>WEBEX</h2>

1. <h5>Countdown Timer</h5>

**Problem question** - Get the flag once the countdown timer reaches zero!However, the minimum time you can set for the countdown is 100 days, so you might be here for a while.

**Link** - http://web.bcactf.com:49154/

**Hint 1** - <details>Can you manipulate a website's JavaScript?</details>
------

When you visit the given website, it allows you to input no. of days in which the flag get's displayed. The catch here is you can't enter a number any less than 100. There's a "Start Countdown" which starts the countdown to the flag.

If you check the source of the page it gives you the code and the part which interests us is the Javascript code - 

```javascript
<script type="text/javascript">
        var time = 100000;
        var minTime = 100;
        var daysInput = document.getElementById("countdownDays");
        var counter;
        document.getElementById("startButton").onclick = function () {
            startCountDown();
        };
        document.getElementById("minTimeHeader").innerHTML = "Minimum Time: " + minTime + " days";

        daysInput.min = minTime;

        function startCountDown() {
            clearInterval(counter);
            if (daysInput.value < minTime) {
                daysInput.value = minTime;
            }
            time = daysInput.value * 24 * 60 * 60;
            counter = setInterval(countdown, 1000);
        }

        function countdown() {
            time -= 1;
            if (time <= 0) {
                getFlag();
                clearInterval(counter);
                return;
            }
            var numdays = Math.floor(time / 86400);
            var numhours = Math.floor((time % 86400) / 3600);
            var numminutes = Math.floor(((time % 86400) % 3600) / 60);
            var numseconds = ((time % 86400) % 3600) % 60;
            document.getElementById("remainingTime").innerHTML = numdays + " Days " + numhours + " Hours " + numminutes + " Minutes " + numseconds + " Seconds";
        }
    </script>
```

When you examine the JS code carefully, the condition if (time <= 0) triggers the getFlag() funtion
As the hint says, we can edit JS here, so we start the timer, and declare the value of time=0 in the console of Inspect Element which gives us the flag

Flag - bcactf{1_tH1nK_tH3_CtF_w0u1D_b3_0v3r_bY_1O0_dAy5}


2. Home Automation - 

Problem question - Check out my super secure home automation system! No, don't try turning the lights off...

link - http://web.bcactf.com:49155/

Hint 1 - How do websites know who you are?
Hint 2 - What's on the table?

This is a basic cookie problem, you visit the website and log in as a guest. On opening Inspect element and you see the cookie with the following value


When you try to turn the lights off it says you need to be the admin, just change the value from vampire to admin and turn off the lights which gives you the flag

flag -  bcactf{c00k13s_s3rved_fr3sh_fr0m_th3_smart_0ven_cD7EE09kQ}



3. Movie-Login-1

Problem question -  I heard a new movie was coming out... apparently it's supposed to be the SeQueL to "Gerard's First Dance"? Is there any chance you can help me find the flyer?

link - http://web.bcactf.com:49160/

Hint 1 - Are the inputs sanitized?

This is a basic SQL injection problem

We input “ ‘ or 1=1--” as the username, which ends the sql syntax and makes the statement true giving us access to the flag

flag - bcactf{s0_y0u_f04nd_th3_fl13r?}


4. Agent Gerald - 

Problem question -  Agent Gerald is a spy in SI-6 (Stegosaurus Intelligence-6). We need you to infiltrate thistop-secret SI-6 webpage, but it looks like it can only be accessed by Agent Gerald's special browser...

link - http://web.bcactf.com:49156/

Hint 1 - What is a way webpages know what kind of browser you're using?

The way websites know the browser we're using is the header “User-Agent” which we send in http request to the server
We could use the inspect element to send a request with a modified User-Agent value
Open the network tab in Inspect element, edit and resend the “/” request with the “User-Agent: Agent Gerald" value
The response should have the flag

flag - bcactf{y0u_h@ck3d_5tegos@urus_1nt3lligence}


5. Movie-Login-2

Problem question -  It's that time of year again! Another movie is coming out, and I really want to get some insider information. I heard that you leaked the last movie poster, and I was wondering if you could do it again for me?  

link - http://web.bcactf.com:49153/

Hint 1 - What steps are they taking to prevent an injection?
Hint 2 - Check the denylist maybe?

Content of file attached - 
"1", "0", "/", "="

This is similar to Movie-Login-1 but this time there's some input sanitation. The file provided gives us the the inputs getting sanatised

So we modify our input to be -
' or true--

which still has the same meaning as the previous payload

flag - bcactf{h0w_d1d_y0u_g3t_h3r3_th1s_t1m3?!?}


6. Movie-Login-3

Problem question -  I think the final addition to the Gerard series is coming out! I heard the last few movies got their poster leaked. I'm pretty sure they've increased their security, though. Could you help me find the poster again?

link - http://web.bcactf.com:49162/

Hint 1 - Does there seem to be anything different about this problem?
Hint 2 - How can you get around the new keywords being detected?

Content of file attached - 
"and",
    "1",
    "0",
    "true",
    "false",
    "/",
    "*",
    "=",
    "xor",
    "null",
    "is",
    "<",
    ">"


This is similar to Movie-Login-2 but this time there's some more input sanitation. The file provided gives us the the inputs getting sanatised

So we modify our input to be -
' OR 2 LIKE 2--

here “2 LIKE 2” gives us the boolean value TRUE , and -- comments out rest of the sql command

flag - bcactf{gu3ss_th3r3s_n0_st0pp1ng_y0u!}


