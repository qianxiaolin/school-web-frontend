<template>
    <div class="chat-window">
      <div class="top">
        <div class="head-pic">
            <div class="head-portrait">
                <img :src="imgUrl" alt="">
            </div>
        </div>
        <div class="info-detail">
          <div class="name">frinedInfo.name </div>
          <div class="detail">frinedInfo.detail </div>
        </div>
        <div class="other-fun">
          <span class="iconfont icon-shipin"> </span>
          <span class="iconfont icon-gf-telephone"></span>
          <label for="docFile">
            <span class="iconfont icon-wenjian"></span>
          </label>
          <label for="imgFile">
            <span class="iconfont icon-tupian"></span>
          </label>
          <input
            type="file"
            name=""
            id="imgFile"
            @change="sendImg"
            accept="image/*"
          />
          <input
            type="file"
            name=""
            id="docFile"
            @change="sendFile"
            accept="application/*,text/*"
          />
          <!-- accept="application/*" -->
        </div>
      </div>
      <div class="botoom">
        <div class="chat-content" ref="chatContent">
          <div class="chat-wrapper" v-for="item in chatList" :key="item.id">
            <div class="chat-friend" v-if="item.uid !== '1001'">
              <div class="chat-text" v-if="item.chatType == 0">
                {{ item.msg }}
              </div>
              <div class="chat-img" v-if="item.chatType == 1">
                <img
                  :src="item.msg"
                  alt="表情"
                  v-if="item.extend.imgType == 1"
                  style="width: 100px; height: 100px"
                />
                <el-image :src="item.msg" :preview-src-list="srcImgList" v-else>
                </el-image>
              </div>
              <div class="chat-img" v-if="item.chatType == 2">
                <div class="word-file">
                  <FileCard
                    :fileType="item.extend.fileType"
                    :file="item.msg"
                  ></FileCard>
                </div>
              </div>
              <div class="info-time">
                <img :src="item.headImg" alt="" />
                <span>name</span>
                <span>time</span>
              </div>
            </div>
            <div class="chat-me" v-else>
              <div class="chat-text" v-if="item.chatType == 0">
                {{ item.msg }}
              </div>
              <div class="chat-img" v-if="item.chatType == 1">
                <img
                  :src="item.msg"
                  alt="表情"
                  v-if="item.extend.imgType == 1"
                  style="width: 100px; height: 100px"
                />
                <el-image
                  style="max-width: 300px; border-radius: 10px"
                  :src="item.msg"
                  :preview-src-list="srcImgList"
                  v-else
                >
                </el-image>
              </div>
              <div class="chat-img" v-if="item.chatType == 2">
                <div class="word-file">
                  <FileCard
                    :fileType="item.extend.fileType"
                    :file="item.msg"
                  ></FileCard>
                </div>
              </div>
              <div class="info-time">
                <span>张三</span>
                <span>2021-6-7</span>
                <img :src="item.headImg" alt="" />
              </div>
            </div>
          </div>
        </div>
        <div class="chatInputs">
          <div class="" @click="clickEmoji">
            <img src="" alt="" />
          </div>
          <div class="emoji-content">
            <Emoji
            ></Emoji>
          </div>
          <input class="inputs" v-model="inputMsg" @keyup.enter="sendText" />
          <div class="send boxinput" @click="sendText">
            <img src="" alt="" />
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        chatList: [],
        inputMsg: "",
        showEmoji: false,
        friendInfo: {},
        srcImgList: [],
      };
    },
    }
  </script>
  
  <style lang="less" scoped>
  .chat-window {
    width: 100%;
    height: 100%;
    margin-left: 20px;
    position: relative;
  
    .top {
      margin-bottom: 10px;
    //   background-color: red;
      &::after {
        content: "";
        display: block;
        clear: both;
      }
      .head-pic {
        float: left;
      }
      .info-detail {
        float: left;
        margin: 5px 20px 0;
        .name {
          font-size: 20px;
          font-weight: 600;
          color: #fff;
        }
        .detail {
          color: #9e9e9e;
          font-size: 12px;
          margin-top: 2px;
        }
      }
      .other-fun {
        float: right;
        margin-top: 20px;
        span {
          margin-left: 30px;
          cursor: pointer;
        }
        input {
          display: none;
        }
      }
    }
    .botoom {
      width: 100%;
      height: 70vh;
      background-image: linear-gradient(to right, #4facfe 0%, #00f2fe 100%);
      border-radius: 20px;
      padding: 20px;
      box-sizing: border-box;
      position: relative;
      .chat-content {
        width: 100%;
        height: 85%;
        overflow-y: scroll;
        padding: 20px;
        box-sizing: border-box;
        &::-webkit-scrollbar {
          width: 0; /* Safari,Chrome 隐藏滚动条 */
          height: 0; /* Safari,Chrome 隐藏滚动条 */
          display: none; /* 移动端、pad 上Safari，Chrome，隐藏滚动条 */
        }
        .chat-wrapper {
          position: relative;
          word-break: break-all;
          .chat-friend {
            width: 100%;
            float: left;
            margin-bottom: 20px;
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            align-items: flex-start;
            .chat-text {
              max-width: 90%;
              padding: 20px;
              border-radius: 20px 20px 20px 5px;
              background-color: rgb(56, 60, 75);
              color: #fff;
              &:hover {
                background-color: rgb(39, 42, 55);
              }
            }
            .chat-img {
              img {
                width: 100px;
                height: 100px;
              }
            }
            .info-time {
              margin: 10px 0;
              color: #fff;
              font-size: 14px;
              img {
                width: 30px;
                height: 30px;
                border-radius: 50%;
                vertical-align: middle;
                margin-right: 10px;
              }
              span:last-child {
                color: rgb(101, 104, 115);
                margin-left: 10px;
                vertical-align: middle;
              }
            }
          }
          .chat-me {
            width: 100%;
            float: right;
            margin-bottom: 20px;
            position: relative;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            align-items: flex-end;
            .chat-text {
              float: right;
              max-width: 90%;
              padding: 20px;
              border-radius: 20px 20px 5px 20px;
              background-color: rgb(29, 144, 245);
              color: #fff;
              &:hover {
                background-color: rgb(26, 129, 219);
              }
            }
            .chat-img {
              img {
                max-width: 300px;
                max-height: 200px;
                border-radius: 10px;
              }
            }
            .info-time {
              margin: 10px 0;
              color: #fff;
              font-size: 14px;
              display: flex;
              justify-content: flex-end;
  
              img {
                width: 30px;
                height: 30px;
                border-radius: 50%;
                vertical-align: middle;
                margin-left: 10px;
              }
              span {
                line-height: 30px;
              }
              span:first-child {
                color: rgb(101, 104, 115);
                margin-right: 10px;
                vertical-align: middle;
              }
            }
          }
        }
      }
      .chatInputs {
        width: 90%;
        position: absolute;
        bottom: 0;
        margin: 3%;
        display: flex;
        .boxinput {
          width: 50px;
          height: 50px;
          background-color: rgb(66, 70, 86);
          border-radius: 15px;
          border: 1px solid rgb(80, 85, 103);
          position: relative;
          cursor: pointer;
          img {
            width: 30px;
            height: 30px;
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
          }
        }
        .emoji {
          transition: 0.3s;
          &:hover {
            background-color: rgb(46, 49, 61);
            border: 1px solid rgb(71, 73, 82);
          }
        }
  
        .inputs {
          width: 90%;
          height: 50px;
          background-image: linear-gradient(120deg, #89f7fe 0%, #66a6ff 100%);
          border-radius: 15px;
          border: 2px solid rgb(34, 135, 225);
          padding: 10px;
          box-sizing: border-box;
          transition: 0.2s;
          font-size: 20px;
          color: #fff;
          font-weight: 100;
          margin: 0 20px;
          &:focus {
            outline: none;
          }
        }
        .send {
          background-color: rgb(29, 144, 245);
          border: 0;
          transition: 0.3s;
          box-shadow: 0px 0px 5px 0px rgba(0, 136, 255);
          &:hover {
            box-shadow: 0px 0px 10px 0px rgba(0, 136, 255);
          }
        }
      }
    }
  }
  </style>