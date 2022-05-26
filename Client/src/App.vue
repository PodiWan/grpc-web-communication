<template>
  <LandingPage :msg="'gRPC response: ' + greeting"/>
</template>

<script>
import LandingPage from './components/LandingPage.vue'
import { GreeterClient } from './greet_grpc_web_pb'
import { HelloRequest } from './greet_pb'

export default {
  name: 'App',
  components: {
    LandingPage
  },
  data: function() {
    return {
      greeting: ""
    };
  },
  created: async function() {
    this.client = new GreeterClient("http://127.0.0.1:8080", null, null);
    let requestHello = new HelloRequest();
      requestHello.setName('ms cop');
    let call = this.client.sayHello(requestHello, {}, (err, response) => {
        this.greeting = response.array[0];
      });
    for(let _ = 0; _ < 10; _++) {
      console.log(await call.requestStream.writeAsync(new HelloRequest()));
      await call.responseStream.moveNext();
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
