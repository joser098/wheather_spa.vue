<template>
  <div class="about">
    <h1 class="comment_title" >Write a comment</h1>
    <textarea name="" id="" placeholder="Comment Here" cols="30" rows="10" class="textarea"></textarea>
    <button class="btn_comment">Send comment</button>
  </div>
</template>

<style>
.about {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
  border-left: 2px solid rgba(253, 242, 242, 0.986);
  padding: 10px 0px;
  background-color: rgba(255, 255, 255, 0.8);
  padding: 10px;
  border-radius: 0px 10px 10px 0px;
}

.textarea {
  border: none;
  width: 60%;
  border-radius: 5px;
  margin: 10px 0px;
}

.btn_comment {
  border: none;
  color: #000;
  background: #fff;
  height: 25px;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
}

.btn_comment:hover {
  box-shadow: 3px 0px 20px rgba(0, 0, 0, 0.1)
}
</style>
