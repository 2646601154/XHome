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
// 间距系统
$spacing-sm: 8px;
$spacing-md: 16px;
$spacing-lg: 24px;
$spacing-xl: 32px;
$spacing-2xl: 48px;

// 颜色系统
$bg-dark: #17171a;
$bg-card: #242424;
$border-color: #444;
$text-muted: #9e9e9e;

.container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    padding: $spacing-md;
    background-color: $bg-dark;
    color: #f5f5f5;

    .card {
        width: 100%;
        max-width: 800px;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: $spacing-lg;
        border-radius: $spacing-lg;
        padding: $spacing-2xl $spacing-xl;
        background-color: $bg-card;
        box-shadow: 0 4px 24px rgba(0, 0, 0, 0.4);

        .avatar {
            width: 180px;
            height: 180px;
            border-radius: 50%;
            background-color: #f5f5f5;
            flex-shrink: 0;

            img {
                width: 100%;
                height: 100%;
                border-radius: 50%;
                object-fit: cover;
            }
        }

        h1 {
            font-size: 36px;
            font-weight: bold;
            text-align: center;
        }

        > p {
            font-size: 18px;
            text-align: center;
            color: $text-muted;
        }

        .item-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: $spacing-md;

            .item {
                min-width: 100px;
                padding: $spacing-sm $spacing-md;
                border: 1px solid $border-color;
                border-radius: $spacing-sm;
                display: flex;
                justify-content: center;
                align-items: center;
                cursor: default;
                transition: all 0.25s ease;

                &:hover {
                    transform: scale(1.08);
                    border-color: #666;
                    background-color: rgba(255, 255, 255, 0.05);
                }
            }
        }

        footer {
            display: flex;
            justify-content: center;
            gap: $spacing-md;
            padding-top: $spacing-md;
            border-top: 1px solid rgba(255, 255, 255, 0.08);
            width: 100%;

            p {
                font-size: 14px;
                color: $text-muted;
            }
        }
    }
}

// 弹窗遮罩层
.modal-mask {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.6);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
    animation: fadeIn 0.2s ease;
}

// 弹窗内容层
.modal-content {
    width: 90%;
    max-width: 400px;
    background: $bg-card;
    border-radius: $spacing-md;
    padding: $spacing-lg;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
}

// 弹窗头部
.modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-bottom: $spacing-md;
    margin-bottom: $spacing-lg;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);

    h3 {
        margin: 0;
        color: #f5f5f5;
    }
}

.close-btn {
    border: none;
    background: transparent;
    font-size: 22px;
    color: $text-muted;
    cursor: pointer;
    width: 32px;
    height: 32px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 50%;
    transition: all 0.2s;

    &:hover {
        background: rgba(255, 255, 255, 0.1);
        color: #f5f5f5;
    }
}

// 弹窗内容
.modal-body {
    text-align: center;
}

.email-text {
    font-size: 16px;
    color: #ccc;
    margin: 0 0 $spacing-lg;
    letter-spacing: 1px;
    user-select: all;
}

.copy-btn {
    padding: $spacing-sm $spacing-lg;
    background: #409eff;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 14px;
    transition: background 0.2s;

    &:hover {
        background: #66b1ff;
    }
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}
</style>
