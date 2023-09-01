<template>
  <h1>Deep Chat</h1>
  <!-- initialMessages is an example of passing a data object into a property -->
  <!-- directConnection is an example of passing an object directly into a property -->

  <deep-chat
    :introMessage="introMessage"
    :request="{
      url: 'http://localhost:5050/ask',
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
    }"
    :containerStyle="{
      borderRadius: '10px',
      position: 'fixed',
      bottom: '0px',
      right: '7%',
      zIndex: '1',
    }"
  >
  </deep-chat>
</template>

<script>
import "deep-chat";

export default {
  name: "App",
  data() {
    return {
      request: this.request,
      response: this.reponse,
      introMessage: "Hi I am your AI assistant, ask me anything!",
    };
  },
  method: {
    requestInterceptor(request) {
      console.log(request);
      request.body = { prompt: request.body.messages[0].text };
      return request;
    },
    responseInterceptor(response) {
      console.log(response);
      const responseText = response.messages;
      return { result: { text: responseText } };
    },
  },
};
</script>

<style>
div {
  font-family: sans-serif;
  text-align: center;
}

deep-chat {
  display: flex;
  justify-content: center;
}
</style>
