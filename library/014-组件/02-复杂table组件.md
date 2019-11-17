#### 负责table组件
> 利用element组件，直接进行修改

```
<el-table
        :data="tableData"
        :span-method="objectSpanMethod"
        border
        style="width: 100%; margin-top: 20px">
        <el-table-column label="区域">
          <el-table-column
            prop="id"
            label="消耗及综合能耗"
            width="120"/>
          <el-table-column
            prop="date"
            label="#"
            width="40"/>
        </el-table-column>
        <el-table-column
          label="加热"
          align="center"><el-table-column
            prop="name"
            label="煤气"/>
          <el-table-column
            prop="amount1"
            label="电"/>
          <el-table-column
            prop="amount2"
            label="软水"/>
          <el-table-column
            prop="amount3"
            label="氮气"/>
          <el-table-column
            label="空气"/>
          <el-table-column
            label="产生蒸汽"/>
          <el-table-column
            label="外送蒸汽"/>
          <el-table-column
            label="综合能耗"/>
          <el-table-column
            label="基准"/>
        </el-table-column>
      </el-table>


      <script>
      export default {
        data() {
          return {
            tableData: [
              {
                date: '早',
                id: '日期',
                name: '王小虎',
                amount1: '234',
                amount2: '3.2',
                amount3: 10
              },
              {
                date: '中',
                id: '日期',
                name: '王小虎',
                amount1: '165',
                amount2: '4.43',
                amount3: 12
              },
              {
                date: '夜',
                id: '日期',
                name: '王小虎',
                amount1: '324',
                amount2: '1.9',
                amount3: 9
              },
              {
                date: '天',
                id: '日期',
                name: '王小虎',
                amount1: '621',
                amount2: '2.2',
                amount3: 17
              }
            ]
          }
        },
        methods: {
          objectSpanMethod({ row, column, rowIndex, columnIndex }) {
            if (columnIndex === 0) {
              if (rowIndex === 0) {
                return {
                  rowspan: 4,
                  colspan: 1
                }
              } else {
                return {
                  rowspan: 0,
                  colspan: 0
                }
              }
            }
          }
        }
      }
      </script>      
```
![alt文本](amWiki/images/table.jpg "复杂table组件")
