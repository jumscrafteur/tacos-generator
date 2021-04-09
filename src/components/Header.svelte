<div class="header">
    <img src="/images/logo_text.svg" alt="" height="52px" class="logo" />
    <img src="/images/folder.svg" alt="" height="14px" class="icon disabled" />
</div>

<style lang="scss">
    @import "../styles/vars";
    .header {
        width: 100%;
        height: 78px;

        background-color: $primary;
        box-shadow: 0px 2px 0px 0px rgba(29, 29, 27, 0.1);

        & .logo {
            position: relative;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }

        & .icon {
            position: relative;
            float: right;
            top: 50%;
            right: 14px;
            transform: translate(0, -50%);
        }
    }
</style>
