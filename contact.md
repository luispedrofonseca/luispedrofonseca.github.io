---
layout: single
title: "Contact"
permalink: /contact/
author_profile: true
---
Please get in touch using the form below. Feel free to reach me through <a href="http://www.twitter.com/lpfonseca" target="_blank">Twitter</a> as well.

<style>
.feedback-input {
  color:#3c3c3c;
  font-weight:500;
  font-size: 14px;
  border-radius: 0;
  background-color: #efefef;
  padding: 13px 13px 13px 54px;
  margin-bottom: 10px;
  width:100%;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  -ms-box-sizing: border-box;
  box-sizing: border-box;
  border: 3px solid rgba(0,0,0,0);
}

/* Icons ---------------------------------- */
#contact_name{
  background-image: url(/static/images/contact-form/name.svg);
  background-size: 30px 30px;
  background-position: 11px 8px;
  background-repeat: no-repeat;
}

#contact_email{
  background-image: url(/static/images/contact-form/email.svg);
  background-size: 30px 30px;
  background-position: 11px 8px;
  background-repeat: no-repeat;
}

#contact_comment{
  background-image: url(/static/images/contact-form/comment.svg);
  background-size: 30px 30px;
  background-position: 11px 8px;
  background-repeat: no-repeat;
}

textarea {
  width: 100%;
  height: 150px;
  line-height: 150%;
  resize:vertical;
}

#button-blue{
  border-width: 0px;
  color: #fff;
  width: 150px;
  height: 40px;
  display: block;
  font-size: 14px;
  line-height: 40px;
  float:left;
  background: #38b7ea;
  -webkit-border-radius: 20px;
  border-radius: 20px;
  -webkit-transition: 0.2s ease;
  -moz-transition: 0.2s ease;
  -ms-transition: 0.2s ease;
  transition: 0.2s ease;
}

</style>

<script type="text/javascript">
  function validateContactForm() 
  {
    var x = document.forms["contact-form"]["email"].value;
    var atpos = x.indexOf("@");
    var dotpos = x.lastIndexOf(".");
    if (atpos<1 || dotpos<atpos+2 || dotpos+2>=x.length) 
    {
        alert("Please insert a valid e-mail address!");
        return false;
    }
  }
</script>

<div>
  <div>
    <form id="contactform" name="contact-form" onsubmit="return validateContactForm();" method="POST">
      <input type="hidden" name="_subject" value="Luis Pedro Fonseca - Contact Form" />
      <input type="hidden" name="_next" value="/about" />
      <input name="name" type="text" class="feedback-input" id="contact_name" placeholder="Name" />
      <input name="email" type="text" class="feedback-input" id="contact_email" placeholder="Email" />
      <textarea name="text" class="feedback-input" id="contact_comment" placeholder="Comment"></textarea>
      <input type="text" name="_gotcha" style="display:none" />
      <input type="submit" value="Send" id="button-blue"/>
    </form>
    <script>
      var contactform =  document.getElementById('contactform');
      contactform.setAttribute('action', 'https://formspree.io/f/luispedrofonseca@gmail.com');
    </script>
  </div>

&nbsp;