 <template>
  <div class="abc">
    <div class="d-nav">
      <div class="d-option" @click="$router.back(-1)">
        <img src alt />返回
      </div>
      <div class="d-infoimg">
        <img src />
      </div>
      <div class="d-name">{{topic.nickname}}</div>
      <div class="btn" v-if="judgeInfor.length == 0" @click="addFriend">关注</div>
      <div class="btn" v-if="judgeInfor.length != 0" @click="deleteFriend">取消关注</div>
    </div>
    <div class="mui-scroll-wrapper scrollstyle">
      <div class="mui-scroll">
        <div class="detail">
          <div class="d-img">
            <mt-swipe>
              <mt-swipe-item v-for="item in topic.img_src" :key="item._id">
                <img :src="'http://47.101.137.209:8899'+item" alt />
              </mt-swipe-item>
            </mt-swipe>
          </div>
          <div class="d-main">
            <div class="d-title">{{topic.title}}</div>
            <div class="d-txt">{{topic.content}}</div>
            <div class="d-tag">{{topic.plate}}</div>
            <div class="d-time">{{topic.created_time | dateFormat}}</div>
          </div>
          <div class="splid"></div>
          <div class="comment">
            <div class="comment_head">评论：{{comments.length}}</div>
            <div class="comment_text">
              <textarea ref="textarea" placeholder="请输入你要评论的内容" maxlength="120"></textarea>
              <button class="comment_btn" @click="commitComment">发表评论</button>
            </div>
            <div class="comment_content" v-for="(comment,index) in comments" :key="comment._id">
              <div class="comment_content_head">
                <div class="commenter_avatar">
                  <img :src="'http://47.101.137.209:8899'+comment.conmmenter_avatar" alt />
                </div>
                <div class="commenter_nickname">{{comment.comment_nickname}}</div>
                <div class="commenter_floor">{{index+1}}楼</div>
              </div>
              <div class="commenter_content">
                <div class="content">{{comment.comment_content}}</div>
              </div>
              <div class="comment_footer">
                <div class="comment_createdtime">{{comment.created_time | dateFormat }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<style lang="less" scoped>
.mint-swipe {
  border-radius: 10px;
  height: 300px;
  margin: 8px;
  border: none;
  box-shadow: 0px 0px 10px -10px black;
  .mint-swipe-item {
    // &:first-child {

    // }
    // &:nth-child(2) {

    // }
    // &:last-child {

    // }

    img {
      width: 100%;
      height: 100%;
      background-size: cover;
    }
  }
}
.scrollstyle {
  margin-top: 50px;
}
.abc {
  height: 100%;
}
.d-nav {
  background-color: white;
  height: 50px;
  width: 100%;
  position: fixed;
  z-index: 999;
  top: 0px;
  .d-option {
    width: 30px;
    height: 30px;
    margin: 10px;
    overflow: hidden;
    float: left;
    line-height: 30px;
    font-size: 15px;
    img {
      width: 100%;
    }
  }
  .d-infoimg {
    width: 40px;
    height: 40px;
    margin: 5px;
    overflow: hidden;
    float: left;
    border-radius: 25px;
    img {
      width: 100%;
      background-size: cover;
    }
  }
  .d-name {
    padding-left: 5px;
    width: 180px;
    float: left;
    height: 50px;
    color: black;
    font-size: 17px;
    line-height: 50px;
    text-align: center;
  }
  .btn {
    width: 70px;
    float: right;
    height: 30px;
    line-height: 30px;
    margin: 10px;
    color: rgb(255, 66, 66);
    font-size: 14px;
    text-align: center;
    border: 1px solid rgb(255, 66, 66);
    border-radius: 25px;
  }
}
.detail {
  margin-bottom: 50px;
  background-color: white;
  width: 100%;
  height: 100%;
  .d-img {
    width: 100%;
    .swiper-item img {
      width: 100%;
      height: 550px;
      background-size: auto;
    }
    .swiper-item img[lazy="loading"] {
      width: 100%;
    }
    .swiper-pagination-fraction {
      width: 20%;
      left: 80%;
    }
  }
  .d-main {
    width: 100%;
    margin-top: 5px;
    .d-title {
      padding-left: 8px;
      width: 100%;
      line-height: 30px;
      font-size: 17px;
      font-weight: bold;
      color: black;
    }
    .d-txt {
      padding: 8px;
      width: 100%;
      font-size: 14px;
      color: rgb(80, 80, 80);
      font-weight: normal;
    }
    .d-tag {
      width: 70px;
      height: 30px;
      line-height: 30px;
      text-align: center;
      background-color: rgb(190, 190, 190);
      border: none;
      border-radius: 15px;
      font-size: 12px;
      color: rgb(100, 100, 255);
      line-height: 30px;
    }
    .d-time {
      font-size: 8px;
      background-color: transparent;
    }
  }
}
.comment {
  margin-top: 10px;
  width: 100%;
  .comment_text {
    width: 100%;
    height: 40px;
    margin-top: 5px;
    textarea {
      float: left;
      width: 80%;
      margin: 0;
      height: 40px;
    }
    .comment_btn {
      float: left;
      width: 20%;
      height: 40px;
      color: black;
    }
  }
  .comment_head {
    width: 100%;
    height: 40px;
    line-height: 40px;
    background: white;
    color: black;
    font-weight: 900;
    padding-left: 10px;
  }
  .comment_content {
    width: 100%;
    margin-top: 5px;
    background: white;
    .comment_content_head {
      width: 100%;
      height: 30px;
      .commenter_avatar {
        float: left;
        width: 30px;
        height: 30px;
        margin-left: 20px;
        img {
          width: 100%;
          height: 100%;
          border-radius: 50%;
        }
      }
      .commenter_nickname {
        float: left;
        width: 50%;
        height: 30px;
        margin-left: 10px;
        line-height: 30px;
        font-size: 15px;
        color: rgb(243, 159, 4);
      }
      .commenter_floor {
        float: right;
        font-size: 10px;
        font-weight: 100;
        line-height: 30px;
        margin-right: 10px;
      }
    }
    .commenter_content {
      width: 100%;
      .content {
        width: 80%;
        margin-left: 60px;
      }
    }
    .comment_footer {
      width: 100%;
      .comment_createdtime {
        width: 80%;
        margin-left: 60px;
        font-size: 10px;
        font-weight: 100;
        color: gray;
      }
    }
  }
}
</style>
<script>
import mui from "@/../lib/mui/js/mui.js";
import myaxios, {
  gettopicById,
  getcomment,
  commitComment,
  addFriendURL,
  judgeFriendURL,
  deleteFriendURL,
  getsessionURL,
  addCollectionURL
} from "@/tools/myaxios.js";
import { Toast } from "mint-ui";
import { async } from "q";
import { EALREADY } from "constants";
export default {
  data: function() {
    return {
      user: "",
      topic: "",
      comments: "",
      judgeInfor: ""
    };
  },
  methods: {
    async commitComment() {
      var comment_content = this.$refs.textarea.value;
      var topic_id = this.$route.params.id;
      let obj = {
        comment_content: comment_content,
        topic_id: topic_id
      };
      if (comment_content) {
        let result = await myaxios("POST", commitComment, obj);
        if (result.data.code == 102) {
          this.$router.push("/login");
          Toast(result.data.message);
        } else if (result.data.code == 101) {
          Toast(result.data.message);
          this.$refs.textarea.value = "";
          var obj2 = {
            _id: this.$route.params.id
          };
          let result2 = await myaxios("POST", getcomment, obj2);
          if (result2.data.code == 101) {
            this.comments = result2.data.comments;
          } else {
            Toast("请求出错请重试！");
          }
        } else {
          Toast(result.data.message);
        }
      } else {
        Toast("评论的内容不能为空哦！！！");
      }
    },
    async addFriend() {
      var friend_nickname = this.topic.nickname;
      var friend_avatar = this.topic.icon;
      var friendID = this.topic.user_id;
      var obj = {
        friend_nickname: friend_nickname,
        friend_avatar: friend_avatar,
        friendID: friendID
      };
      let result = await myaxios("POST", addFriendURL, obj);
      if (result.data.code == 101) {
        Toast("关注成功！");
        var obj = {
          friend_id: this.topic.user_id
        };
        let result2 = await myaxios("POST", judgeFriendURL, obj);
        if (result2.data.code == 101) {
          this.judgeInfor = result2.data.judgeInfor;
        }
      } else {
        this.$router.push("/login");
        Toast(result.data.message);
      }
    },
    async deleteFriend() {
      var obj = {
        friend_id: this.topic.user_id
      };
      let result = await myaxios("POST", deleteFriendURL, obj);
      if (result.data.code == 101) {
        Toast("取消关注成功！");
        this.judgeInfor = "";
      }
    }
  },
  async created() {
    var obj = {
      _id: this.$route.params.id
    };
    let result = await myaxios("POST", gettopicById, obj);
    if (result.data.code == 101) {
      this.topic = result.data.topic;
    } else {
      Toast("请求出错请重试！");
    }
    let result2 = await myaxios("POST", getcomment, obj);
    if (result2.data.code == 101) {
      this.comments = result2.data.comments;
    } else {
      Toast("请求出错请重试！");
    }
    var obj2 = {
      friend_id: this.topic.user_id
    };
    let result3 = await myaxios("POST", judgeFriendURL, obj2);
    if (result3.data.code == 101) {
      this.judgeInfor = result3.data.judgeInfor;
    }
  },
  mounted() {
    mui(".mui-scroll-wrapper").scroll({
      deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
    });
  },
};
</script>
