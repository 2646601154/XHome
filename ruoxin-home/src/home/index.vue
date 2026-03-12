<script setup lang="ts">
import { ref } from "vue"
const email = ref("xiaruoxinby@qq.com")
const showEmailModal = ref(false)

const closeModal = () => {
    showEmailModal.value = false
}
const copyEmail = () => {
    try {
        // 复制文本到剪贴板
        navigator.clipboard.writeText(email.value)
        alert('邮箱复制成功！')
    } catch (err) {
        alert('复制失败，请手动复制：' + email.value)
    }
}
</script>

<template>
    <main class="container">
        <div class="card">
            <div class="avatar">
                <img src="../avatar/myAvatar.jpg" alt="头像">

            </div>
            <h1>Xiaruoxin</h1>
            <p>跨专业学习 Vue3 Java</p>
            <div class="item-container">
                <div class="item">博客</div>
                <div class="item">简历</div>
                <div class="item" @click="showEmailModal = true">邮箱</div>

                <!-- 邮箱弹窗（遮罩层 + 内容层） -->
                <div v-if="showEmailModal" class="modal-mask" @click="closeModal">
                    <div class="modal-content" @click.stop> <!-- stop 阻止事件冒泡到遮罩层 -->
                        <div class="modal-header">
                            <h3>我的邮箱</h3>
                            <button class="close-btn" @click="showEmailModal = false">×</button>
                        </div>
                        <div class="modal-body">
                            <p class="email-text">{{ email }}</p>
                            <button class="copy-btn" @click="copyEmail">一键复制邮箱</button>
                        </div>
                    </div>
                </div>

                <div class="item">github</div>
                <div class="item">bilibili</div>
            </div>
            <footer>
                <p>备案一</p>
                <p>备案二</p>
                <p>备案三</p>
            </footer>
        </div>
    </main>




</template>

<style lang="scss" scoped>
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    padding: 10px 10px;
    background-color: #17171a;
    color: #f5f5f5;



    .card {
        width: 1200px;
        height: 700px;
        border-radius: 20px;
        padding: 20px;
        background-color: #242424;
        //阴影
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);

        .avatar {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            margin: 40px auto;

            background-color: #f5f5f5;

            img {
                width: 100%;
                height: 100%;
                border-radius: 50%;
            }
        }

        h1 {
            font-size: 40px;
            text-align: center;
            //字体加粗

            font-weight: bold;


        }

        .item-container {
            height: 160px;
            display: flex;
            //压缩后换行
            flex-wrap: wrap;
            //justify-content可选的值有：flex-start, flex-end, center, space-between, space-around
            justify-content: space-around;
            align-items: center;

            .item {
                width: 100px;
                height: 50px;
                //边框
                border: 1px solid #444444;
                border-radius: 10px;
                display: flex;
                justify-content: center;
                align-items: center;
                //鼠标移上去后放大
                transition: all 0.3s ease-in-out;

                &:hover {
                    transform: scale(1.1);
                }

                //光标不变
                cursor: default;

                //第三个item


            }

        }

        p {
            font-size: 20px;
            text-align: center;
            margin-top: 20px;
            //浅色字体
            color: #9e9e9e;
        }

        footer {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;

        }
    }
}

/* 弹窗遮罩层 */
.modal-mask {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
}

/* 弹窗内容层 */
.modal-content {
    width: 400px;
    background: #242424;
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
    animation: fadeIn 0.3s ease;
}

/* 弹窗头部 */
.modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #eee;
    padding-bottom: 10px;
    margin-bottom: 20px;
}

.modal-header h3 {
    margin: 0;
    color: white;
}

.close-btn {
    border: none;
    background: transparent;
    font-size: 20px;
    color: #999;
    cursor: pointer;
    width: 30px;
    height: 30px;
    line-height: 30px;
    border-radius: 50%;
    transition: background 0.3s;
}

.close-btn:hover {
    background: #f5f5f5;
    color: #666;
}

/* 弹窗内容 */
.modal-body {
    text-align: center;
}

.email-text {
    font-size: 18px;
    color: #333;
    margin: 0 0 20px 0;
    letter-spacing: 1px;
}

.copy-btn {
    padding: 8px 20px;
    background: #409eff;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    transition: background 0.3s;
}

.copy-btn:hover {
    background: #66b1ff;
}

/* 弹窗淡入动画 */
@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(-20px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}
</style>
