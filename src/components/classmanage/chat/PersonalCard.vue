<template>
    <div class="person-card">
        <div class="info">
            <div class="head-portrait">
                <img :src="imgUrl" alt="">
            </div>
            <div class="info-detail">
                <div class="name">张三</div>
                <div class="detail">你在干嘛</div>
            </div>
        </div>
    </div>
</template>
  
<script setup>


</script>
  
<style lang="less" scoped>
.person-card {
    width: 250px;
    height: 80px;
    border-radius: 10px;
    background-color: #1d90f5;
    position: relative;
    margin: 25px 0;
    cursor: pointer;

    .info {
        position: absolute;
        left: 50%;
        top: 50%;
        width: 90%;
        transform: translate(-50%, -50%);
        overflow: hidden;
        display: flex;
        .head-portrait {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border: 2px solid rgb(255, 255, 255);
            position: relative;

            &::before {
                content: '';
                width: 15px;
                height: 15px;
                z-index: 1;
                display: block;
                border-radius: 50%;
                background-color: rgb(144, 225, 80);
                position: absolute;
                right: 0;
            }

            img {
                width: 45px;
                height: 45px;
                border-radius: 50%;
                box-sizing: border-box;
                position: absolute;
                left: 50%;
                top: 50%;
                transform: translate(-50%, -50%);
                vertical-align: middle;
            }
        }

        .info-detail {
            margin-top: 5px;
            margin-left: 20px;
            .name {
                color: #fff;
                overflow: hidden;
                white-space: nowrap;
                text-overflow: ellipsis;
                margin-bottom: 5px;
            }
            .detail {
                color: #fff;
                overflow: hidden;
                white-space: nowrap;
                text-overflow: ellipsis;
                font-size: 12px;
            }
        }
    }
    &:hover {
        
        transition: 0.3s;
        box-shadow: 0px 0px 10px 0px rgba(0, 136, 255);

        .info {
            .info-detail {
                .detail {
                    color: #fff;
                }
            }
        }
    }
}

.activeCard {
    background-color: #1d90f5;
    transition: 0.3s;
    box-shadow: 3px 2px 10px 0px rgba(0, 136, 255);

    .info {
        .info-detail {
            .detail {
                color: #fff;
            }
        }
    }
}</style>