<script>
export let btn = false;
</script>

<div on:click class="item" class:btn><slot></slot></div>

<style>
  .item {
    margin: 10px;
    border-radius: 50%;
    box-shadow: 3px 3px #ebeaea, -1px -1px #fff;
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    user-select: none;
  }
 .btn{
   background:#FF9E0E; 
   color:#fff
  }

  .btn:hover{
    box-shadow: 0 0 10px rgba(0,0,0,0.5)
  }
  .item:hover{
    box-shadow: 0 0 10px rgba(85, 83, 83, 0.2)
  }
  .item :global(img){
    width: 50%;
  }
  .item:active{
   box-shadow: 1px 1px #fff, -1px -1px #ebeaea;
  }
  .btn:active{
   box-shadow: 1px 1px #ffffff, -1px -1px #c1afaf;
  }
</style>