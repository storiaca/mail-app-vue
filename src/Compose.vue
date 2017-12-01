<template>
  <div>
    <a href="#composeModal" data-toggle="modal" class="btn btn-compose">Compose</a>

    <div aria-hidden="true" role="dialog" tabindex="-1" id="composeModal" class="modal fade" style="display: none;">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <button aria-hidden="true" data-dismiss="modal" class="close" type="button">×</button>
            <h4 class="modal-title">New Message</h4>
          </div>

          <div class="modal-body">
            <form role="form" class="form-horizontal" @submit.prevent="sendMessage">
              <div class="form-group">
                <label for="subject" class="col-lg-2 control-label">Subject</label>
                <div class="col-lg-10">
                  <input type="text" id="subject" class="form-control" v-model="message.subject">
                </div>
              </div>

              <div class="form-group">
                <label for="messages" class="col-lg-2 control-label">Messages</label>
                <div class="col-lg-10">
                  <textarea class="form-control" id="message" cols="30" rows="10" v-model="message.content"></textarea>
                </div>
              </div>

              <div class="form-group">
                <div class="col-lg-offset-2 col-lg-10">
                  <button type="submit" class="btn btn-send">Send</button>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import { eventBus } from './main';
  import moment from 'moment';

  export default {
    data() {
      return {
        message: {
          subject: '',
          content: ''
        }
      };
    },
    methods: {
      sendMessage() {
        eventBus.$emit('sentMessage', {
          message: {
            subject: this.message.subject,
            content: this.message.content,
            isDeleted: false,
            type: 'outgoing',
            date: moment(),
            from: {
              name: 'Aleksandar Ristic',
              email: 'info@learnvue.com'
            },
            attachments: []
          }
        });
      }
    }
  }
</script>
