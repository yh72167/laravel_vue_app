<template>
   <body class="page-mypage page-2colum page-logined">
    <!-- メニュー -->

    <p id="js-show-msg" style="display:none;" class="msg-slide">
      <?php echo getSessionFlash('msg_success'); ?>
    </p>

    <!-- メインコンテンツ -->
    <div id="contents" class="site-width">

      <h1 class="page-title">MYPAGE</h1>

      <!-- Main -->
      <section id="main" >
         <section class="list panel-list">
           <h2 class="title" style="margin-bottom:15px;">
            登録商品一覧
           </h2>
           <?php
             if(!empty($productData)):
              foreach($productData as $key => $val):
            ?>
              <a href="registProduct.php<?php echo (!empty(appendGetParam())) ? appendGetParam().'&p_id='.$val['id'] : '?p_id='.$val['id']; ?>" class="panel">
                <div class="panel-head">
                  <img src="<?php echo showImg(sanitize($val['pic1'])); ?>" alt="<?php echo sanitize($val['name']); ?>">
                </div>
                <div class="panel-body">
                  <p class="panel-title"><?php echo sanitize($val['name']); ?> <span class="price">¥<?php echo sanitize(number_format($val['price'])); ?></span></p>
                </div>
              </a>
            <?php
              endforeach;
             endif;
            ?>
         </section>

        <section class="list list-table">
          <h2 class="title">
            連絡掲示板一覧
          </h2>
          <table class="table">
            <thead>
              <tr>
                <th>最新送信日時</th>
                <th>取引相手</th>
                <th>メッセージ</th>
              </tr>
            </thead>
            <tbody>
             <?php
              if(!empty($bordData)){
                foreach($bordData as $key => $val){
                  if(!empty($val['msg'])){
                    $msg = array_shift($val['msg']);
             ?>
                 <tr>
                    <td><?php echo sanitize(date('Y.m.d H:i:s',strtotime($msg['send_date']))); ?></td>
                    <td>◯◯ ◯◯</td>
                    <td><a href="msg.php?m_id=<?php echo sanitize($val['id']); ?>"><?php echo mb_substr(sanitize($msg['msg']),0,40); ?>...</a></td>
                </tr>
             <?php
                  }else{
             ?>
                 <tr>
                    <td>--</td>
                    <td>◯◯ ◯◯</td>
                    <td><a href="msg.php?m_id=<?php echo sanitize($val['id']); ?>">まだメッセージはありません</a></td>
                </tr>
              <?php
                  }
                }
              }
            ?>
            </tbody>
          </table>
        </section>

        <section class="list panel-list">
          <h2 class="title" style="margin-bottom:15px;">
            お気に入り一覧
          </h2>
          <?php
             if(!empty($likeData)):
              foreach($likeData as $key => $val):
            ?>
              <a href="productDetail.php<?php echo (!empty(appendGetParam())) ? appendGetParam().'&p_id='.$val['id'] : '?p_id='.$val['id']; ?>" class="panel">
                <div class="panel-head">
                  <img src="<?php echo showImg(sanitize($val['pic1'])); ?>" alt="<?php echo sanitize($val['name']); ?>">
                </div>
                <div class="panel-body">
                  <p class="panel-title"><?php echo sanitize($val['name']); ?> <span class="price">¥<?php echo sanitize(number_format($val['price'])); ?></span></p>
                </div>
              </a>
          <?php
            endforeach;
           endif;
          ?>
        </section>
      </section>

      <!-- サイドバー -->
      <?php
        require('sidebar_mypage.php');
      ?>
    </div>

    <!-- footer -->
  </body>
</template>
<style>
  #main{
    border: none !important;
  }
  .list{
    margin-bottom: 30px;
  }
</style>
