<template>
    <div class='chart-container'>
      <el-card class='head-card'>
        <!-- ul>li*6>i+p{今日新增用户} -->
        <ul>
          <li>
            <i class='primary'>1</i>
            <p>今日新增用户</p>
          </li>
          <li>
            <i class='primary'>2</i>
            <p>总用户量</p>
          </li>
          <li>
            <i class='danger'>3</i>
            <p>新增试题</p>
          </li>
          <li>
            <i class='danger'>4</i>
            <p>总试题量</p>
          </li>
          <li>
            <i class='success'>5</i>
            <p>总刷题量</p>
          </li>
          <li>
            <i class='success'>6</i>
            <p>人均刷题量</p>
          </li>
        </ul>
      </el-card>
      <el-card class="main-card"></el-card>
    </div>
</template>

<script>
export default {
    name:"chart"
}
</script>

<style lang="less">
  .chart-container{
    .head-card{
      height: 149px;
      .el-card__body{
        padding-top: 10px;
      }
      ul{
        display: flex;
        list-style: none;
        justify-content: space-around;
        align-items: flex-start;
        li{
          i{
            display: block;
            width: 99px;
            height: 99px;
            border-radius: 50%;
            border: 2px solid #000;
            text-align: center;
            line-height: 99px;
            font-style: normal;
            // 生成 i.primary
            &.primary{
              border-color:#0488fa;
              color:#0488fa;
            }
            &.danger{
              border-color:#f76238;
              color:#f76238;
            }
            &.success{
              border-color:#74d691;
              color:#74d691;
            }
          }
          p{
            text-align: center;
            font-size: 16px;
            color:#737373;
            padding-top: 11px;
          }
        }
      }
    }
    // 主体区域
    .main-card{
      margin-top: 13px;
      height: 571px;
    }
  }
</style>