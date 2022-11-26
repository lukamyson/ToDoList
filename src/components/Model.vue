<template>
  <Transition name="model">
    <div class="model" @click="closeModel">
      <div class="model__block" @click.stop="">
        <h2 class="model__title">
          {{ edit ?  words.titlewindowedit[lang] : words.titlewindow[lang]}}
        </h2>
        <div class="model__inputs">
          <label>
            <span>Title</span>
            <input type="text" v-model="title" />
          </label>

          <label>
            <span>Content</span>
            <textarea v-model="descr"></textarea>
          </label>
        </div>
        <div class="model__btns">
          <button class="model__btn cancel" @click="closeModel">{{ words.closebtn[lang]}}</button>
          <button v-if="!edit" class="model__btn add" @click="addNote">
            {{ words.addbtn[lang]}}
          </button>
          <button v-else class="model__btn add" @click="changeNote">
             {{ words.editwindowbtn[lang]}}
          </button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {

  data() {
    return {
      title: "",
      descr: "",
      id: this.currentId,
    };
  },
  inject:['words'],
  props: {
    lang:String,    
    currentId: Number,
    edit: Boolean,
    editNote: Object,
  },

  methods: {
    closeModel() {
      this.$emit("closeModel", false);
      this.title = "";
      this.descr = "";
    },
    addNote() {
      if (this.title != "" && this.descr != "") {
        const item = {
          id: this.id++,
          title: this.title,
          descr: this.descr,
          date: new Date().toLocaleDateString(),
        };
        this.$emit("addNote", item);
        this.title = "";
        this.descr = "";
      }
    },
    changeNote() {
      if(this.title != '' && this.descr != ''){
        const editedNote ={
          id:this.editNote.id,
          title:this.title,
          descr:this.descr,
          date: new Date().toLocaleDateString()
        }
        this.$emit('editedNote', editedNote)
        this.closeModel()
      }
    }
  },
};
</script>

<style>
.model {
  background: rgba(0, 0, 0, 0.35);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 99999;
  display: flex;
  justify-content: center;
  align-items: center;
}
.model__block {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    #fffbfe;
  border-radius: 28px;
  max-width: 312px;
  width: 100%;
  padding: 24px;
}
.model__title {
  color: #1c1b1f;
  font-size: 24px;
  line-height: 32px;
  margin-bottom: 16px;
}
.model__inputs {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
.model__inputs label {
  position: relative;
}
.model__inputs span {
  position: absolute;
  left: 16px;
  top: 8px;
  font-size: 12px;
  line-height: 16px;
  color: #6750a4;
}
.model__inputs input,
.model__inputs textarea {
  background: #e7e0ec;
  border-radius: 4px 4px 0px 0px;
  width: 100%;
  border: none;
  outline: none;
  padding: 23px 0 9px 16px;
  font-size: 16px;
  line-height: 24px;
  color: #49454f;
  border-bottom: 1px solid #1c1b1f;
  resize: none;
}
.model__btns {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
  margin-top: 25px;
}
.model__btn {
  font-size: 14px;
  line-height: 20px;
  font-family: "RM";
  background: transparent;
  padding: 10px 12px;
  text-transform: uppercase;
  transition: backgroung 500ms;
}
.cancel {
  color: #cf1b1b;
}
.cancel:hover {
  background: #ffe1e1;
}
.add {
  color: #6750a4;
}
.add:hover {
  background: #e6ddff;
}

.model-enter-active,
.model-leave-active {
  transition: 0.2s linear;
}

.model-enter-from,
.model-leave-to {
  opacity: 0;
  transform: scale(1.5);
}
</style>