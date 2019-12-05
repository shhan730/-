---
layout: default
title: Contact Long Haul
---

<div id="contact">
  <h1 class="pageTitle">Contact Me</h1>
  <div class="contactContent">
    <p class="intro">이메일을 보내주세요!</p>
    <p>아래 항목들을 기입해서 이메일을 보내주시면 빠르게 답장을 보내드리겠습니다!</p>
  </div>
  <form action="https://formspree.io/heewon.dev@gmail.com" method="POST">
    <label for="name">성함</label>
    <input type="text" id="name" name="name" class="full-width"><br>
    <label for="email">회신받을 이메일 주소</label>
    <input type="email" id="email" name="_replyto" class="full-width"><br>
    <label for="message">내용</label>
    <textarea name="message" id="message" cols="30" rows="10" class="full-width"></textarea><br>
    <input type="submit" value="Send" class="button">
  </form>
</div>
