---
title: 友情链接
---

<div class="post-body">
   <div id="links">
      <style>
         .links-content{
         margin-top:1rem;
         }
         .link-navigation::after {
         content: " ";
         display: block;
         clear: both;
         }
         .card {
         width: 45%;
         font-size: 1rem;
         padding: 10px 20px;
         border-radius: 4px;
         transition-duration: 0.15s;
         margin-bottom: 1rem;
         display:flex;
         }
         .card:nth-child(odd) {
         float: left;
         }
         .card:nth-child(even) {
         float: right;
         }
         .card:hover {
         transform: scale(1.1);
         box-shadow: 0 2px 6px 0 rgba(0, 0, 0, 0.12), 0 0 6px 0 rgba(0, 0, 0, 0.04);
         }
         .card a {
         border:none;
         }
         .card .ava {
         width: 3rem!important;
         height: 3rem!important;
         margin:0!important;
         margin-right: 1em!important;
         border-radius:4px;
         }
         .card .card-header {
         font-style: italic;
         overflow: hidden;
         width: 100%;
         }
         .card .card-header a {
         font-style: normal;
         color: #2bbc8a;
         font-weight: bold;
         text-decoration: none;
         }
         .card .card-header a:hover {
         color: #d480aa;
         text-decoration: none;
         }
         .card .card-header .info {
         font-style:normal;
         color:#a3a3a3;
         font-size:14px;
         min-width: 0;
         overflow: hidden;
         white-space: nowrap;
         }
      </style>
      <div class="links-content">
         <div class="link-navigation">
            <div class="card">
               <img class="ava" src="https://poems-kanro.oss-cn-hangzhou.aliyuncs.com/DZCVkmrpqWfdv3h.jpg" />
               <div class="card-header">
                  <div>
                     <a href="https://www.kanromiku.top/">Kanromiku’s blog</a>
                  </div>
                  <div class="info">Kanromiku的杂货铺</div>
               </div>
            </div>
            <!-- <div class="card">
               <img class="ava" src="$avatar" />
               <div class="card-header">
                  <div>
                     <a href="$url">$name</a>
                  </div>
                  <div class="info">$info</div>
               </div>
            </div> -->
         </div>
      </div>
   </div>
</div>

友链申请-->[邮箱](mailto:leiyiming@rayminn.top)或在评论区留言，请附上网站名称、地址、简介和头像链接。

# 友链朋友圈

<!-- 挂载友链朋友圈的容器 -->
<div class="post-content">
<div id="cf-container">Loading...</div>
</div>
<!-- 加样式和功能代码 -->
<!-- 将apiurl改成你后端生成的api地址 -->
<script type="text/javascript">
  var fdataUser = {
    apiurl: 'https://friends-circle.rayminn.top/'
  }
</script>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/Rayminn/img/cdn/fcircle.css">
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/Rayminn/img/cdn/fcircle-rb.js"></script>