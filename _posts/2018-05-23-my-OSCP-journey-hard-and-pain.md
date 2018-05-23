---
layout: post
title: "My OSCP Journey is dense and painful"
date: 2018-05-23
excerpt: "My experience during the journey towards certification OSCP"
tags: [it security, OSCP, blog, english]
comments: true
---
**Watch out!** This is post using english language, if you find bahasa version see this [Indonesian Version](http://mirfansulaiman.github.io/perjalanan-oscp-yang-padat-dan-menyakitkan)
{: .notice}

## Introduction
<figure>
	<a href="https://kaizensecurity.files.wordpress.com/2016/05/oscp-certs.png"><img src="https://kaizensecurity.files.wordpress.com/2016/05/oscp-certs.png"></a>
</figure>

Alhamdulillah, I finally got another chance to blogging, after so long after my personal website removed because I cant pay hosting bills and domain (Ups) wkwkkwk. And now I decided to use [github pages](https://pages.github.com/) as my personal website :)

Okay,i want to tell you a little about my experience during the trip to OSCP certification, in 2014 I had a dream to get this OSCP certification because I heard from my friends in [forum](http://www.indonesianbacktrack.or.id/forum/index.php), I believe that having this certification is the greatest thing in achieving being a [penetration testing IT expert](https://en.wikipedia.org/wiki/Penetration_test) because it's not easy to get it, but in this year 2018 coinciding in [ramadhan holy month](https://en.wikipedia.org/wiki/Ramadan) alhamdulillah I had the opportunity to realize my dream 4 years ago. What a valuable thing in my life, because dreams come true. I am really grateful to Allah swt and [PT Vantage Point Indonesia](http://vantagepoint.co.id/) who has helped me realize my dream.

Basicly, i am programmer, not expert not noob hmm ya midle :D , i interested IT Security since i am in junior high school and now continues studiy at universities in jakarta and doing final task (undergraduate thesis) ! 

Before starting I read many blogs about oscp exam, one of which belongs to my office friend [Wen bin](https://kongwenbin.wordpress.com/2017/02/23/officially-oscp-certified/) and also blog my shifu [Matias prasodjo](https://gauli.com/oscp-certification-review/) and many more.

## OSCP Lab Internal

Okay before taking the OSCP exam I took the 90 days lab, starting on March 18, 2018 and it should be finished on June 18th. But because there is a special request from My boss and at the month of June there is a schedule for my test in school then I took the exam in May this month. for my training option I took a 90 day lab access and the fact is I only 2 months studied on the lab then took exam.

<figure>
	<a href="https://www.offensive-security.com/wp-content/uploads/2014/12/offsec-playground-thumb-21.jpg"><img src="https://www.offensive-security.com/wp-content/uploads/2014/12/offsec-playground-thumb-21.jpg"></a>
</figure>

In this internal lab there are dozens of computer machines that we can hack with different operating systems, Believe it is for you who will take the OSCP exam would be nice to finish all the machines in this lab because many methods and ways that will instantly be useful when exam or real world :) 

Learning OSCP while doing the thesis is really painful, because the focus needs to be divided into two. But for 2 months I share the time between working on OSCP lab and doing my undergraduate thesis.

the machine I got before the exam is alice, phoenix, mike, barry, payday, ralph, pain, leftturn, bethany, beta, gamma, bob, tophat, dotty, sherlock, gh0st, fc4, helpdesk, susie, oracle, kraken, hotline, punchout, master, jeff, joe, jd, mail, kevin, core, sean, nicky, brett. 

Total 33 Machines.

## OSCP Exam

Go to exam.
In this exam I perform fasting, so do not eat or drink during the test.
even fasting just drinking water. And for food i bought with Go-food.

I schedule an exam on May 20, 2018 at 00:00 on the start of that date, which means it's midnight on a Saturday night. All the preparations I have prepared before starting, ranging from tools that would otherwise be used and small notes.

<figure>
	<a href="/images/exam-date-full.PNG"><img src="/images/exam-date-full.PNG"></a>
	<figcaption>Exam Booking Date</figcaption>
</figure>

However, I booked for the exam in May that it was full, so I had to change the test date or wait for the students who canceled the exam schedule. Well here I created a simple python script to check every 5 minutes whether the student canceled his exam schedule in May. After I get the test date, I want to share this script but after talking with the offensive-security party whether to make the robot to check the exam schedule automatically it turns out something like this is prohibited. So I undo the intention to share the script. hehehe <i>peace</i>

Before the exam begin, I am reading the instructions and rules for this exam in here [Exam Guide](https://support.offensive-security.com/#!oscp-exam-guide.md) need to remember the instructions and the rules about exam can changes at any time so read the instructions again 3 hours before the start of the exam !. 

The time given in this exam is 24 hours, there are only 6 machines given to me 1 machine just as a debugger to test exploit stack overflow. Every each machine have different points, the highest point is 25 points and the smallest is 10 points.

To pass the exam required 70 points from 100 points, If only 65 points can be assisted bonus points from the report of the internal lab results of at least 10 machines with different methods of attack and finishing the exercise that are on the pwk module (Penetresting with Kali-linux ) and the bonus point value is 5 points. Very helpful if the lack of points to pass.

When the exam starts, I got an offensive-security email about login access for the exam and the dashboard URL of the exam control panel. This control panel have an objective that we must finish it along with the form to submit the contents of local.txt and proof.txt files.

Here is the timeline of my progress in the exam, more or less like this: 

Timeline :
* 00:00 am - 02:00 am : Information Gathering, scanning ports in every machine.
* 02:00 am - 04:00 am : Successfully pawning 1 machine +10 point
* 04:00 am - 05:00 am : Rest, eat sahur + pray shubuh.
* 05:00 am - 06:00 am : Successfully pawning 1 stack overflow +25 point machine
* 06:00 am - 09:00 am : Sleeping, sleeping, sleeping.
* 09:00 am - 12:00 am : Successfully pawning 1 machine +20 point
* 12:00 pm - 13:00 pm : Dzuhur Prayer + Shower
* 13:00 pm - 17:00 pm : enum, enum, enum
* 17:00 pm - 20:20 pm : Successfully pawning 1 machine +25 point
* 20:20 pm - 21:30 pm : enum, enum, enum last machine.
* 21:30 pm - END      : I overslept at my desk so I could not finish the last machine with a point value of 20

At 17:00 pm - 20:20 pm actually I'm not focused anymore here, I'm worried and afraid will be fail in this exam. Since I have not been in a safe position, I have to hack 1 more machine to pass. While did not focus my hands trembling, headed like there are birds flying around my head, I finally take a break about 5 minutes to clear the brain temporarily because in that time I have not managed to do privelege escalation on the third machine, only get low shell. Finally after enumerating slowly I managed to get root access on the machine :)

<figure>
	<a href="https://78.media.tumblr.com/412e18b8c19a1cc75f77b0d4f672073c/tumblr_p16yf0SkWa1tsyxa7o1_500.gif"><img src="https://78.media.tumblr.com/412e18b8c19a1cc75f77b0d4f672073c/tumblr_p16yf0SkWa1tsyxa7o1_500.gif"></a>
</figure>

Finally I can finish 4 machines with the total points is 80 points, is enough to pass this exam :) although I regret due to overslept but i am very happy to pass it :) and the consequently I miss sahur to eat i dont eat until 3am to 6pm 

Then the next day I made a report to send to offensive-security in accordance with the format specified on the following page [Submission Instructions](https://support.offensive-security.com/#!oscp-exam-guide.md) because if not in accordance with the provisions of any one then our report will be rejected and will automatically fail.

After 2 days then I get the email from offensive-security :

<figure>
	<a href="/images/oscp-exam-result.PNG"><img src="/images/oscp-exam-result.PNG"></a>
	<figcaption>Penetration Testing with Kali Linux - OSCP Certification Exam Results - OS-XXXXXX</figcaption>
</figure>

Wow, I am pass !! 

<figure>
	<a href="https://lh3.googleusercontent.com/CBMuZb8_mEFh46IQM2UGM2Pu-AlPkGJECx1QLphn0bQ=w688-h264-no"><img src="https://lh3.googleusercontent.com/CBMuZb8_mEFh46IQM2UGM2Pu-AlPkGJECx1QLphn0bQ=w688-h264-no"></a>
	<figcaption>YES I AM TRIED HARDER !</figcaption>
</figure>

## Suggestions
1. Make sure your condition is fit and not sick, keep your health condition because your brain will be forced to work 24 hours.
	<figure>
		<a href="/images/oscp-brain-talking.jpg"><img src="/images/oscp-brain-talking.jpg"></a>
		<figcaption>Brain Talking</figcaption>
	</figure>
2. Understand the basics of networking and programming.
3. Make sure your time is specific to OSCP, so your focus is only for OSCP. Honestly take OSCP while create the undergraduate thesis is not good !!
4. Complete all the exercises in the pwk module and 10 machines on lab to get bonus points. Unless you are sure enough to pass the exam, myself only send the test report just because I have not finished the exercises in the pwk module because it is too focused on the internal lab.
5. Sleep enough.
6. Beleive

## Thank you note.
As gratitude I would like to thank the family who have supported me throughout this OSCP until exams are over, Thanks to my girlfriend whom remind me to take some food to eat at sahur and at Maghrib during exam (It will be fun if you have girlfriend :D ), and of course for my friends from work [Vantage Point Security Singapore](http://vantagepoint.sg/) & [Vantage Point Security Indonesian](http://vantagepoint.co.id/) Wen bin, Eka Tan, Ryan, JK, Saed, David Harley, Wira, Suman, James, David, dan tuyen whom give me a spirit and motivation. Especially for Paul Craig who has provided accommodation during the exam and give me a motivation so far also very kindness.

and for my 

## Note

The translate powered by [g00gle Translate](https://translate.google.com/)