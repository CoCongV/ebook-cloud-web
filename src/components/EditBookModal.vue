<template>
  <div>
    <!-- <a-button type="primary" @click="showModal">Open Modal with async logic</a-button> -->
    <a-icon type="edit" @click="showModal"></a-icon>
    <a-modal
      title="Title"
      :visible="visible"
      @ok="handleOk"
      :confirmLoading="confirmLoading"
      @cancel="handleCancel"
    >
    <a-form>
      <a-form-item label="name">
          <a-input></a-input>
      </a-form-item>
    </a-form>
    <template slot="footer">
        <a-button key="back" @click="handleCancel">关闭</a-button>
        <a-button key="submit" @click="handleOk" type="primary">提交</a-button>
    </template>
    </a-modal>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        visible: false,
        confirmLoading: false,
      };
    },
    methods: {
        showModal() {
            this.visible = true;
        },
      handleOk(_) {
        this.confirmLoading = true;
        setTimeout(() => {
          this.visible = false;
          this.confirmLoading = false;
        }, 2000);
      },
      handleCancel(_) {
        console.log('Clicked cancel button');
        this.visible = false;
      },
    },
  };
</script>