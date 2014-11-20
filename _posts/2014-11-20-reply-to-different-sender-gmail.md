---
layout: post
title: "Reply To user via C#"
description: "C# programming"
headline: mail sender
categories: 
  - engineering 
  - "web development"
tags: mail ReplyTo
imagefeature: 
imagecredit: 
imagecreditlink: 
comments: true
mathjax: false
featured: true
published: true
---

I worked for a client for him we have made a support page to get the feedback from the Page. Where the user will submit the query which will be send to the client.
The client just reply back to the user. But the problem is we are using gmail account to send mail to the client and when the client reply backs its not reaching the user its was coming to us.

{% highlight java %} 

private static Task MailSender( string to = "user@gmail.com", string replyTo = "customer@gmail.com", string message="test message", string subject = "Test Subject")
{
	const string emailServer = "smtp.gmail.com";
	const string emailUser = "reports@gmail.com";
	const string emailPassword = "passoword";

	var mailMsg = new System.Net.Mail.MailMessage();

	// To
	mailMsg.To.Add(new System.Net.Mail.MailAddress(to, ""));

	// From
	mailMsg.From = new System.Net.Mail.MailAddress("donotreply@gmail.com", "Product Support");
			  
	//mailMsg.ReplyTo = new MailAddress(replyTo);//obsolute
	mailMsg.ReplyToList.Add(new MailAddress(replyTo));
	
	// Subject and multipart/alternative Body
	mailMsg.Subject = subject;
	string html = message;
	mailMsg.AlternateViews.Add( System.Net.Mail.AlternateView.CreateAlternateViewFromString( html, null, System.Net.Mime.MediaTypeNames.Text.Html));

	// Init SmtpClient and send
	var smtpClient = new System.Net.Mail.SmtpClient(emailServer, Convert.ToInt32(587));
	var credentials = new System.Net.NetworkCredential(emailUser, emailPassword);
	smtpClient.Credentials = credentials;
	smtpClient.EnableSsl = true;
	//smtpClient.Send(mailMsg);
	return Task.Factory.StartNew(() = smtpClient.SendAsync(mailMsg, "token"));
}

{% endhighlight %}

On Adding the given line we are getting the reply to client directly as given below.
{% highlight java%}
	//mailMsg.ReplyTo = new MailAddress(replyTo);//obsolute
	mailMsg.ReplyToList.Add(new MailAddress(replyTo));
{% endhighlight %}
![ReplytoImage](/images/ReplytoImage.png)
