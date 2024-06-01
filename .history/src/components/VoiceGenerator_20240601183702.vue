<template>
  <div class="container mt-5">
    <div class="card shadow-sm">
      <div class="card-header bg-primary text-white text-center">
        <h2>语音生成器</h2>
      </div>
      <div class="card-body">
        <div class="form-group">
          <label for="textInput">输入文字内容</label>
          <textarea class="form-control" id="textInput" v-model="text" rows="3" placeholder="输入要生成语音的文字内容"></textarea>
        </div>
        <div class="form-group">
          <label for="roleSelect">选择角色</label>
          <select class="form-control" id="roleSelect" v-model="selectedRole">
            <option v-for="role in roles" :key="role" :value="role">{{ role }}</option>
          </select>
        </div>
        <button class="btn btn-primary btn-block" @click="generateVoice">确定</button>
        <div v-if="audioUrl" class="mt-4 text-center">
          <audio controls class="w-100" :src="audioUrl"></audio>
          <button class="btn btn-success mt-2" @click="downloadVoice">下载</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: '',
      selectedRole: '',
      roles: ['角色1', '角色2', '角色3'],
      audioUrl: ''
    };
  },
  methods: {
    async generateVoice() {
      // 将 text 和 selectedRole 发送到 API 以生成语音
      const response = await fetch('API_ENDPOINT', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          text: this.text,
          role: this.selectedRole
        })
      });
      const data = await response.json();
      this.audioUrl = data.audioUrl; // 假设 API 返回生成语音的 URL
    },
    downloadVoice() {
      const link = document.createElement('a');
      link.href = this.audioUrl;
      link.download = 'generated-voice.mp3';
      link.click();
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 600px;
}
.card {
  border-radius: 10px;
}
</style>
