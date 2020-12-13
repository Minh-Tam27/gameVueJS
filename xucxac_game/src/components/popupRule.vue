<template>
    <div class="wrapper-popup" v-bind:class="getClassPopup">
        <div class="rule">
            <h3>Luật chơi</h3>
            <p>
              Người chơi: PLAYER 1 và PLAYER 2. Hãy set điểm chiến thắng ở FINAL SCORE trước nhé! <br style="margin-bottom: 3px;">
              Có 2 xúc xắc để quay trong trò chơi, mỗi lần quay điểm của xúc sắc được tính ở CURRENT, 
              tổng điểm của PLAYER được hiển thị ngay dưới tên PLAYER. <br style="margin-bottom: 3px;"><strong>Chú ý:</strong> Khi PLAYER quay 1 trong 2 xúc xắc 
              vào 1 điểm CURRENT nhận được là 0, nghĩa là + 0 vào điểm tổng. <br style="margin-bottom: 3px;"> Bấm ROLL DICE để quay xúc xắc, HOLD để dừng lượt.
            </p>
            <button 
                v-on:click="confirmButton" class="confirm">Đã hiểu</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'popup-rule',
    props: {
        isOpenPopup: { type: Boolean, default: false }
    },
    data() {
        return {
        }
    },
    methods:{
        confirmButton(){
            this.$emit('handleConfirm');
        }
    },
    computed: {
        getClassPopup: function() {
            return {
                'open-popup': this.isOpenPopup
            }
        }
    }
}
</script>

<style>
    .wrapper-popup {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background-color: rgba(0,0,0,0.4);
        opacity: 0;
        visibility: hidden;
        transition: all .3s ease;
    }
    .wrapper-popup.open-popup {
        opacity: 1;
        visibility: visible;
    }
    .rule {
        width: 350px;
        padding: 20px;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%) scale(1.2);
        background-color: #fff;
        position: absolute;
        font-family: 'Courier New', Courier, monospace;
        transition: all .3s ease;
    }
    .open-popup .rule {
        transform: translate(-50%, -50%) scale(1);
    }
    .rule h3 {
        background-color: #333;
        color: #fff;
        font-size: 27px;
        margin-bottom: 10px;
    }
    .rule .confirm {
        cursor: pointer;
        font-family: Arial, Helvetica, sans-serif;
        font-size: 12px;
        margin-top: 20px;
        padding: 8px 15px;
        border: 2px solid #333;
        background-color: #fff;
        transition: all .3s ease;
    }
    .rule .confirm:hover {
        color: #fff;
        background-color: #333;
    }
</style>