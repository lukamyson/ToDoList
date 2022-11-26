<template>
  <div class="notes__item">
    <div class="notes__item-top" :class="{between: !grid}">
      <h3 class="notes__item-title">{{note.title}}</h3>
      <p class="notes__item-date">{{note.date}}</p>
    </div>
    <p class="notes__item-text">{{note.descr}}</p>
      
    
    <div class="notes__item-btns">
      <button class="notes__item-btn edit" @click="$emit('changeNote', note.id)">
        <img src="@/assets/img/edit.svg" alt="" />
        <span>{{ words.editbtn[lang]}}</span>
      </button>
      <button class="notes__item-btn dei" @click="$emit('delNote',note.id)">
        <img src="@/assets/img/dei.svg" alt="" />
        <span>{{ words.deledit[lang]}}</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
    inject:['words'],
     
     props:{
        lang:String,
        grid:Boolean,
        note:Object,
        
     },
     
};
</script>

<style>
.notes__item {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.05),
      rgba(103, 80, 164, 0.05)
    ),
    #fffbfe;

  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.3),
    0px 1px 3px 1px rgba(0, 0, 0, 0.15);
  border-radius: 16px;
  padding: 16px 16px 28px 16px;
}
.notes__item-title {
  font-size: 16px;
  line-height: 24px;
  font-family: "RM";
}
.notes__item-date {
  color: #cac4d0;
  font-size: 14px;
  line-height: 20px;
  letter-spacing: 0.25px;
}
.notes__item-text {
  font-size: 14px;
  line-height: 20px;
  color: #49454f;
  margin-top: 15px;
  margin-bottom: 30px;
}
.notes__item-btns {
  display: flex;
  justify-content: flex-end;
  gap: 15px;
}
.notes__item-btn {
  display: flex;
  align-items: center;
  gap: 10px;
  background:  transparent;
  padding: 12px;
  border-radius: 5px;
}
.notes__item-btn span{
  font-size: 14px;
  line-height: 20px;
  font-family: "RM";
}
.edit {
  color: #6750A4;
}
.edit:hover{
    
background: #E6DDFF;
}
.dei{
    color: #CF1B1B;
}
.dei:hover{
    background: #FFE1E1;
}
.between  {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

</style>


