<template>
    <div class="wap-main">
      <!--  点击群组，群组资料页面  -->
      <div class="wap-main-group" v-if="active_group">
        <div class="wap-add-friend-title">
        <span class="wap-main-chat-title-back" @click="active_group=false">
          <Icon type="ios-arrow-back" size="18"/>
        </span>
          <span class="wap-main-chat-title-name">
          聊天信息({{group_list.length}})
        </span>
        </div>
        <div class="wap-group-info">
          <div v-for="group in group_list">
            <div class="wap-group-info-logo">
              <img :src="group.logo" alt="">
            </div>
            <div class="wap-group-info-name">
              {{group.name}}
            </div>
          </div>
        </div>
      </div>

      <!-- 退出群组，模态框 -->

    </div>

</template>

<script>
    export default {
        name: "WapChat",
      mounted() {
        if(!this.$User.name){
          this.$router.push('/login')
        }else{

          this.getChat();
        }
      },
      data(){
        return {
          chat_data: {},
          send_message: '',               // 发送消息内容
          send_image: null,               // 选择发送图片
          emoji_active: false,            // 表情包

          // 第三方网站
          active_frame: null,

          // 用户消息列表
          message_data: {
            1: [
              {'name': 'test', 'logo': '/static/images/index.png', 'message': 'hello', 'add_time': '8:50'},
              {'name': 'xiaoxin', 'logo': '/static/images/index.png', 'message': 'hello', 'add_time': '8:51'},
              {'name': 'test2', 'logo': '/static/images/index.png', 'message': 'hello', 'add_time': '8:52'},
              {'name': 'test3', 'logo': '/static/images/index.png', 'message': 'hello', 'add_time': '8:53'},
            ],
            2: [
              {'id': 2, 'name': 'admin', 'logo': '/static/images/admin.jpg', 'message': 'hello', 'add_time': '8:50'},
              {'id': 1, 'name': 'xiaoxin', 'logo': '/static/images/xiaoxin.jpg', 'message': 'hello', 'add_time': '8:51'},
              {'id': 2, 'name': 'admin', 'logo': '/static/images/admin.jpg', 'message': 'hello', 'add_time': '8:52'},
              {'id': 1, 'name': 'xiaoxin', 'logo': '/static/images/xiaoxin.jpg', 'message': '你好，你知道我是谁吗？或许你并不知道，或许你刚认识我，或许你并不了解我，或许你自己都不了解自己', 'add_time': '8:53'},
              {'id': 2, 'name': 'admin', 'logo': '/static/images/admin.jpg', 'message': 'hello', 'add_time': '8:52'},
              {'id': 1, 'name': 'xiaoxin', 'logo': '/static/images/xiaoxin.jpg', 'message': '你好，你知道我是谁吗？或许你并不知道，或许你刚认识我，或许你并不了解我，或许你自己都不了解自己', 'add_time': '8:53'},
              {'id': 2, 'name': 'admin', 'logo': '/static/images/admin.jpg', 'message': 'hello', 'add_time': '8:52'},
              {'id': 1, 'name': 'xiaoxin', 'logo': '/static/images/xiaoxin.jpg', 'message': '你好，你知道我是谁吗？或许你并不知道，或许你刚认识我，或许你并不了解我，或许你自己都不了解自己', 'add_time': '8:53'},
              {'id': 2, 'name': 'admin', 'logo': '/static/images/admin.jpg', 'message': 'hello', 'add_time': '8:52'},
              {'id': 1, 'name': 'xiaoxin', 'logo': '/static/images/xiaoxin.jpg', 'message': '你好，你知道我是谁吗？或许你并不知道，或许你刚认识我，或许你并不了解我，或许你自己都不了解自己', 'add_time': '8:53'},
              {'id': 2, 'name': 'admin', 'logo': '/static/images/admin.jpg', 'message': 'hello', 'add_time': '8:52'},
              {'id': 1, 'name': 'xiaoxin', 'logo': '/static/images/xiaoxin.jpg', 'message': '你好，你知道我是谁吗？或许你并不知道，或许你刚认识我，或许你并不了解我，或许你自己都不了解自己', 'add_time': '8:53'},
            ]
          },

          // 表情包
          emoji_list: [
            {'url': '1.gif', 'name': '#1'}, {'url': '2.gif', 'name': '#2'},
            {'url': '3.gif', 'name': '#3'}, {'url': '4.gif', 'name': '#4'},
            {'url': '5.gif', 'name': '#5'}, {'url': '6.gif', 'name': '#6'},
            {'url': '7.gif', 'name': '#7'}, {'url': '8.gif', 'name': '#8'},
            {'url': '9.gif', 'name': '#9'}, {'url': '10.gif', 'name': '#10'},
            {'url': '11.gif', 'name': '#11'}, {'url': '12.gif', 'name': '#12'},
            {'url': '13.gif', 'name': '#13'}, {'url': '14.gif', 'name': '#14'},
            {'url': '15.gif', 'name': '#15'}, {'url': '16.gif', 'name': '#16'},
            {'url': '17.gif', 'name': '#17'}, {'url': '18.gif', 'name': '#18'},
            {'url': '19.gif', 'name': '#19'}, {'url': '20.gif', 'name': '#20'},
            {'url': '21.gif', 'name': '#21'}, {'url': '22.gif', 'name': '#22'},
            {'url': '23.gif', 'name': '#23'}, {'url': '24.gif', 'name': '#24'},
            {'url': '25.gif', 'name': '#25'}, {'url': '26.gif', 'name': '#26'},
            {'url': '27.gif', 'name': '#27'}, {'url': '28.gif', 'name': '#28'},
            {'url': '29.gif', 'name': '#29'}, {'url': '30.gif', 'name': '#30'},
            {'url': '31.gif', 'name': '#31'}, {'url': '32.gif', 'name': '#32'},
            {'url': '33.gif', 'name': '#33'}, {'url': '34.gif', 'name': '#34'},
            {'url': '35.gif', 'name': '#35'}, {'url': '36.gif', 'name': '#36'},
            {'url': '37.gif', 'name': '#37'}, {'url': '38.gif', 'name': '#38'},
            {'url': '39.gif', 'name': '#39'}, {'url': '40.gif', 'name': '#40'},
            {'url': '41.gif', 'name': '#41'}, {'url': '42.gif', 'name': '#42'},
            {'url': '43.gif', 'name': '#43'}, {'url': '44.gif', 'name': '#44'},
            {'url': '45.gif', 'name': '#45'}, {'url': '46.gif', 'name': '#46'},
            {'url': '47.gif', 'name': '#47'}, {'url': '48.gif', 'name': '#48'},
            {'url': '49.gif', 'name': '#49'}, {'url': '50.gif', 'name': '#50'},
            {'url': '51.gif', 'name': '#51'}, {'url': '52.gif', 'name': '#52'},
            {'url': '53.gif', 'name': '#53'}, {'url': '54.gif', 'name': '#54'},
            {'url': '55.gif', 'name': '#55'}, {'url': '56.gif', 'name': '#56'},
            {'url': '57.gif', 'name': '#57'}, {'url': '58.gif', 'name': '#58'},
            {'url': '59.gif', 'name': '#59'}, {'url': '60.gif', 'name': '#60'},
            {'url': '61.gif', 'name': '#61'}, {'url': '62.gif', 'name': '#62'},
            {'url': '63.gif', 'name': '#63'}, {'url': '64.gif', 'name': '#64'},
            {'url': '65.gif', 'name': '#65'}, {'url': '66.gif', 'name': '#66'},
            {'url': '67.gif', 'name': '#67'}, {'url': '68.gif', 'name': '#68'},
            {'url': '69.gif', 'name': '#69'}, {'url': '70.gif', 'name': '#70'},
            {'url': '71.gif', 'name': '#71'}, {'url': '72.gif', 'name': '#72'},
            {'url': '73.gif', 'name': '#73'}, {'url': '74.gif', 'name': '#74'},
            {'url': '75.gif', 'name': '#75'}, {'url': '76.gif', 'name': '#76'},
            {'url': '77.gif', 'name': '#77'}, {'url': '78.gif', 'name': '#78'},
            {'url': '79.gif', 'name': '#79'}, {'url': '80.gif', 'name': '#80'},
            {'url': '81.gif', 'name': '#81'}, {'url': '82.gif', 'name': '#82'},
            {'url': '83.gif', 'name': '#83'}, {'url': '84.gif', 'name': '#84'},
            {'url': '85.gif', 'name': '#85'}, {'url': '86.gif', 'name': '#86'},
            {'url': '87.gif', 'name': '#87'}, {'url': '88.gif', 'name': '#88'},
            {'url': '89.gif', 'name': '#89'}, {'url': '90.gif', 'name': '#90'},
            {'url': '91.gif', 'name': '#91'}, {'url': '92.gif', 'name': '#92'},
            {'url': '93.gif', 'name': '#93'}, {'url': '94.gif', 'name': '#94'},
            {'url': '95.gif', 'name': '#95'}, {'url': '96.gif', 'name': '#96'},
            {'url': '97.gif', 'name': '#97'}, {'url': '98.gif', 'name': '#98'},
            {'url': '99.gif', 'name': '#99'}, {'url': '100.gif', 'name': '#100'},
            {'url': '101.gif', 'name': '#101'}
          ],
        }
      },
      methods:{
        // 点击给好友发消息
        clickSendMessage(){

        },

        // 发送消息
        sendMessage(){
          let data = {
            'name': 'xiaoxin',
            'logo': '/static/images/xiaoxin.jpg',
            'message': this.send_message
          };
          this.message_data[this.chat_active_id].push(data);
          this.send_message = '';
          // let div = document.getElementById('chat-body');
          // div.scrollTop = div.scrollHeight;
          this.scrollAuto();
        },

        // 聊天对象是群组或者单个用户
        async addChat(chat_obj){
          let resp = await addChat(chat_obj);
          console.log(resp);
          if(resp.code === 200){
            this.chat_list.unshift(resp.data);
            this.chat_active = true;
          }else{
            this.$Message.warning(resp.message);
          }
        },

        // 聊天更多信息
        chatMore(){

        },

        // 点击表情
        clickEmoji(emoji) {
          this.send_message += '<img src="' + '/static/images/emoji/' + emoji.url + '">';
          this.emoji_active = false;
          setTimeout(() => {
            this.keepLastIndex(document.getElementById('send-message'))
          }, 5)
        },

        // 输入消息
        changeMessage(e) {
          let obj = e.target;
          console.log(obj.innerHTML);
          console.log(obj);
          this.send_message = obj.innerHTML.trim();
          setTimeout(() => {
            this.keepLastIndex(obj)
          }, 5)
        },

        // 聊天滚动条在最底部
        scrollAuto(){
          this.$nextTick(() => {
            let div = document.getElementById('chat-body');
            div.scrollTop = div.scrollHeight;
          })
        },

        // 解决输入框焦点问题
        keepLastIndex(obj){
          let range = null;
          if (window.getSelection) { //ie11 10 9 ff safari
            obj.focus(); //解决ff不获取焦点无法定位问题
            range = window.getSelection(); //创建range
            range.selectAllChildren(obj); //range 选择obj下所有子内容
            range.collapseToEnd(); //光标移至最后
          } else if (document.selection) { //ie10 9 8 7 6 5
            //var range = document.selection.createRange(); //创建选择对象
            range = document.body.createTextRange();
            range.moveToElementText(obj); //range定位到obj
            range.collapse(false); //光标移至最后
            range.select();
          }
        },

        // 选择图片
        clickImage(){
          document.getElementById('send-image').click();
        },

        // 发送图片
        async uploadImage(){
          let input = document.getElementById('send-image');
          let file = input.files[0];
          let formData = new FormData();
          formData.append('file', file);
          let resp = await uploadLogo(formData);
          console.log(resp);
          if (resp.code === 200){
            this.common_logo = resp.data.url;        // 返回的是头像路径
          }
          if(this.create_group_modal){
            this.new_group_logo =  this.$Server + this.common_logo;
          }
        },

        /*------------------  socketio交互 -----------------*/
        send(data){
          console.log('send.......');
          this.$socket.emit('message', 'data')
        }
      },
      sockets:{
        connect: function(){
          console.log('socket connected')
        },
        message: function(){
          console.log('返回' + val)
        }
      },
    }
</script>

<style scoped>

</style>
