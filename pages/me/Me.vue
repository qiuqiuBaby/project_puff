<template>
    <view class="content">
        <!-- 教练基本信息 -->
        <view class="user-msg" @click="personalData">
            <image class="head-portrait" src="/static/image/me/photo.png"></image>
            <view class="name-phone">
                <view class="name-msg">
                    <view class="name">用户6278632</view>
                    <view class="name-icon">
                        <image src="/static/image/me/name-icon.png" class="icon"></image>
                    </view>
                </view>
                <view class="phone">15625564251</view>
            </view>
        </view>
        <!-- 战队和我的学员 -->
        <view class="team-student">
            <view class="team" @click="myTeam">
                <view class="team-icon">
                    <image src="/static/image/me/coach.png" class="icon"></image>
                </view>
                <view class="word">
                    <view class="title">我的房间</view>
                    <view class="describe">查看房间信息</view>
                </view>
            </view>
            <view class="student" @click="teamNumber">
                <view class="student-icon">
                    <image src="/static/image/me/certificate.png" class="icon"></image>
                </view>
                <view class="word">
                    <view class="title">我的房源</view>
                    <view class="describe">查看房源列表</view>
                </view>
            </view>
        </view>

        <!-- 教练认证和进入用户端 -->
        <view class="operation">
            <view class="operation-authentication">
                <image src="/static/image/me/certificate.png" class="icon"></image>
                <view class="word">房东认证</view>
                <view class="finish">已认证</view>
                <uni-icons type="forward" size="12" class="uni-icon"></uni-icons>
            </view>
            <view class="client">
                <image src="/static/image/me/certificate.png" class="icon"></image>
                <view class="word">修改密码</view>
                <uni-icons type="forward" size="12" class="uni-icon"></uni-icons>
            </view>
        </view>

        <!-- 退出登录bun -->
        <view class="logoutBtn" @click="logout">
            <button>退出登录</button>
        </view>
    </view>
</template>
<script>
// uni-id的云对象
const say = uniCloud.importObject('index')
const getToken = uniCloud.importObject('loginToken') // 导入云对象
const uniIdCo = uniCloud.importObject('uni-id-co', {
    customUI: true
})
export default {
    components: {},
    data() {
        return {
            personMsg: {}, //个人资料
        }
    },
    onShow() {
        this.getPersonMsg()
        uni.hideTabBar()
    },
    methods: {
        //获取个人资料
        getPersonMsg() {
            
        },
        //我的战队
        myTeam() {
            //查看是否加入战队
            getBattalion().then(res => {
                // 还没有加入战队 转跳战队列表页面
                if (res.data.code === 0) {
                    uni.navigateTo({
                        url: '/pages/coachMy/teamList'
                    })
                }
                //加入过战队 跳转战队成员页面
                if (res.data.code === 1) {
                    uni.navigateTo({
                        url: '/pages/coachMy/teamNumber'
                    })
                }
            })
        },
        //我的学员
        teamNumber() {
            uni.navigateTo({
                url: '/pages/coachStudent/index'
            })
        },
        //个人资料
        personalData() {
            uni.navigateTo({
                url: '/pages/coachMy/personalData'
            })
        },
        //退出登录
        async logout() {
            // await uniIdCo.logout()
            uni.removeStorage({key: 'uni_id_token'});
            uni.removeStorage({key: 'uni_id_token_expired'});
            uni.removeStorage({key: 'uni-id-pages-userInfo'});
            uni.redirectTo({url: "/uni_modules/uni-id-pages/pages/login/login-withoutpwd"});
            console.log('退出登录')
        }
    }
}
</script>
  
<style lang="scss" scoped>
.content {
    padding-top: 80rpx;
    height: 428rpx;
    width: 100%;
    background: linear-gradient(to left, #e0f9f8, #ebf9f7, #ecfaf5);
}

.user-msg {
    display: flex;
    padding-left: 48rpx;
    margin-bottom: 68rpx;

    .head-portrait {
        max-width: 108rpx;
        height: 108rpx;
        border-radius: 50%;
        //border: 1px solid black;
    }

    .name-phone {
        margin-left: 16rpx;
        display: flex;
        flex-direction: column;
        justify-content: center;

        .name-msg {
            display: flex;
            height: 44rpx;
            align-items: center;

            .name {
                font-size: 32rpx;
                font-weight: 500;
                color: #000000;
            }

            .name-icon {
                display: flex;
                margin-left: 12rpx;
                height: 44rpx;
                align-items: center;

                .icon {
                    padding-top: 0 !important;
                    width: 28rpx;
                    height: 28rpx;
                }
            }
        }

        .phone {
            color: #808080;
            font-size: 14px;
            margin-top: 8rpx;
            font-weight: 400;
        }
    }
}

.team-student {
    display: flex;
    padding: 62rpx 0 0 64rpx;
    width: 710rpx;
    height: 192rpx;
    background: #ffffff;
    border-radius: 6rpx;
    margin: 0 auto;

    .team {
        display: flex;

        .team-icon {
            .icon {
                padding-top: 0 !important;
                width: 72rpx;
                height: 68rpx;
            }
        }

        .word {
            display: flex;
            flex-direction: column;
            margin-left: 18rpx;

            .title {
                font-size: 28rpx;
                font-weight: 500;
                color: #2c2c2c;
            }

            .describe {
                font-size: 24rpx;
                font-weight: 400;
                color: #ababab;
            }
        }
    }

    .student {
        display: flex;
        margin-left: 120rpx;

        .student-icon {
            .icon {
                padding-top: 0 !important;
                width: 68rpx;
                height: 68rpx;
            }
        }

        .word {
            display: flex;
            flex-direction: column;
            margin-left: 18rpx;

            .title {
                font-size: 28rpx;
                font-weight: 500;
                color: #2c2c2c;
            }

            .describe {
                font-size: 24rpx;
                font-weight: 400;
                color: #ababab;
            }
        }
    }
}

.operation {
    padding: 32rpx 0 0 26rpx;
    width: 710rpx;
    height: 208rpx;
    background: #ffffff;
    border-radius: 6rpx;
    margin: 16rpx auto 0;

    .operation-authentication {
        display: flex;
        align-items: center;
        margin-bottom: 64rpx;

        .icon {
            padding-top: 0 !important;
            width: 38rpx;
            height: 40rpx;
        }

        .word {
            margin-left: 10rpx;
            font-size: 28rpx;
            font-weight: 400;
            color: #2c2c2c;
        }

        .finish {
            width: 432rpx;
            margin-left: 32rpx;
            font-size: 28rpx;
            font-weight: 400;
            color: #808080;
            direction: rtl;
        }
    }

    .client {
        display: flex;

        .icon {
            padding-top: 0 !important;
            width: 36rpx;
            height: 40rpx;
        }

        .word {
            width: 206rpx;
            margin-left: 16rpx;
            font-size: 28rpx;
            font-weight: 400;
            color: #2c2c2c;
        }

        .uni-icon {
            margin-left: 380rpx;
        }
    }
}

.logoutBtn {
    width: 70%;
    margin: 20rpx auto;
    font-size: 56rpx;
    font-weight: 400;
}
</style>
  