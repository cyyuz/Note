

<table>
    <tr> <!-- 第一行数据 -->
        <th colspan="1">功能</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
        <th colspan="1">操作</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
        <th colspan="1">描述</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
    </tr>
    <tr> <!-- 第二行数据 -->
        <th rowspan="3"> 撤销 </th>
        <th colspan="1">u</th>
        <th colspan="1"> 撤销最近的操作，多次按下，撤销多个操作 </th>
    </tr>
    <tr>
        <th colspan="1">Ctrl+r</th>
        <th colspan="1"> 恢复上一步被撤销的操作 </th>
    </tr>
    <tr>
        <th colspan="1">:u!</th>
        <th colspan="1"> 撤销所有修改 </th>
    </tr>
    <tr> <!-- 注释 -->
        <th rowspan="12"> 光标移动 </th>
        <th colspan="1">h</th>
        <th colspan="1"> 向左移动一个字符 </th>
    </tr>
    <tr>
        <th colspan="1">l</th>
        <th colspan="1"> 向右移动一个字符 </th>
    </tr>
    <tr>
        <th colspan="1">j</th>
        <th colspan="1"> 向下移动一行 </th>
    </tr>
    <tr>
        <th colspan="1">k</th>
        <th colspan="1"> 向上移动一行 </th>
    </tr>
    <tr>
        <th colspan="1">b</th>
        <th colspan="1"> 向前移动一个单词 </th>
    </tr>
    <tr>
        <th colspan="1">w</th>
        <th colspan="1"> 向后移动一个单词 </th>
    </tr>
    <tr>
        <th colspan="1">e</th>
        <th colspan="1"> 光标跳转到本单词的尾部 </th>
    </tr>
    <tr>
        <th colspan="1">0</th>
        <th colspan="1"> 移动到行首 </th>
    </tr>
    <tr>
        <th colspan="1">$</th>
        <th colspan="1"> 移动到行尾 </th>
    </tr>
    <tr>
        <th colspan="1">gg</th>
        <th colspan="1"> 移动到首行 </th>
    </tr>
    <tr>
        <th colspan="1">gg</th>
        <th colspan="1"> 移动到末行 </th>
    </tr>
    <tr>
        <th colspan="1">:n</th>
        <th colspan="1"> 光标移动到第n行 </th>
    </tr>
    <tr> <!-- 注释 -->
        <th rowspan="4"> 翻页 </th>
        <th colspan="1">Ctrl+b</th>
        <th colspan="1"> 向上翻一页 </th>
    </tr>
    <tr>
        <th colspan="1">Ctrl+f</th>
        <th colspan="1"> 向下翻一页 </th>
    </tr>
    <tr>
        <th colspan="1">Ctrl+u</th>
        <th colspan="1"> 向上翻半页 </th>
    </tr>
    <tr>
        <th colspan="1">Ctrl+d</th>
        <th colspan="1"> 向下翻半页 </th>
    </tr>
    <tr> <!-- 注释 -->
        <th rowspan="5"> 查找 </th>
        <th colspan="1">/test</th>
        <th colspan="1"> 查找test </th>
    </tr>
    <tr>
        <th colspan="1">n</th>
        <th colspan="1"> 下一个查找内容 </th>
    </tr>
    <tr>
        <th colspan="1">N</th>
        <th colspan="1"> 上一个查找内容 </th>
    </tr>
    <tr>
        <th colspan="1">/\ctest</th>
        <th colspan="1"> 忽略大小写，查找test </th>
    </tr>
    <tr>
        <th colspan="1">/\btest</th>
        <th colspan="1"> 查找整个单词，而不是部分匹配 </th>
    </tr>
    <tr> <!-- 注释 -->
        <th rowspan="6"> 插入 </th>
        <th colspan="1">i</th>
        <th colspan="1"> 在光标所在位置前面插入 </th>
    </tr>
    <tr>
        <th colspan="1">a</th>
        <th colspan="1"> 在光标所在位置后面插入 </th>
    </tr>
    <tr>
        <th colspan="1">o</th>
        <th colspan="1"> 在光标所在行的下面插入空白行</th>
    </tr>
    <tr>
        <th colspan="1">O</th>
        <th colspan="1"> 在光标所在行的上面插入空白行 </th>
    </tr>
    <tr>
        <th colspan="1">I</th>
        <th colspan="1"> 在光标所在行的行首插入 </th>
    </tr>
    <tr>
        <th colspan="1">A</th>
        <th colspan="1"> 在光标所在行的行末插入 </th>
    </tr>
    <tr> <!-- 注释 -->
        <th rowspan="6"> 插入 </th>
        <th colspan="1">i</th>
        <th colspan="1"> 在光标所在位置前面插入 </th>
    </tr>
    <tr>
        <th colspan="1">a</th>
        <th colspan="1"> 在光标所在位置后面插入 </th>
    </tr>
    <tr>
        <th colspan="1">o</th>
        <th colspan="1"> 在光标所在行的下面插入空白行</th>
    </tr>
    <tr>
        <th colspan="1">O</th>
        <th colspan="1"> 在光标所在行的上面插入空白行 </th>
    </tr>
    <tr>
        <th colspan="1">I</th>
        <th colspan="1"> 在光标所在行的行首插入 </th>
    </tr>
    <tr>
        <th colspan="1">A</th>
        <th colspan="1"> 在光标所在行的行末插入 </th>
    </tr>
    <tr> <!-- 注释 -->
        <th rowspan="6"> 剪切</th>
        <th colspan="1">x</th>
        <th colspan="1"> 剪切光标所在位置的一个字符 </th>
    </tr>
    <tr>
        <th colspan="1">3x</th>
        <th colspan="1"> 剪切光标所在位置开始的3个字符 </th>
    </tr>
    <tr>
        <th colspan="1">dw</th>
        <th colspan="1"> 剪切光标所在位置到本单词结尾的字符 </th>
    </tr>
    <tr>
        <th colspan="1">D</th>
        <th colspan="1"> 剪切本行光标所在位置后的全部内容 </th>
    </tr>
    <tr>
        <th colspan="1">dd</th>
        <th colspan="1"> 剪切光标所在行 </th>
    </tr>
    <tr>
        <th colspan="1">3dd</th>
        <th colspan="1"> 剪切光标所在行开始的3行 </th>
    </tr>
        <tr> <!-- 注释 -->
        <th rowspan="2"> 复制</th>
        <th colspan="1">yy</th>
        <th colspan="1"> 光标所在行复制到缓冲区 </th>
    </tr>
    <tr>
        <th colspan="1">3yy</th>
        <th colspan="1"> 光标所在行开始的3行复制到缓冲区 </th>
    </tr>
    </tr>
        <tr> <!-- 注释 -->
        <th rowspan="2"> 粘贴</th>
        <th colspan="1">p</th>
        <th colspan="1"> 将缓冲区里的内容粘贴到光标所在位置 </th>
    </tr>
    <tr>
        <th colspan="1">:set paste</th>
        <th colspan="1"> 粘贴模式，不自动换行 </th>
    </tr>
    </tr>
        <tr> <!-- 注释 -->
        <th rowspan="4"> 替换</th>
        <th colspan="1">r</th>
        <th colspan="1"> 替换光标所在位置的一个字符 </th>
    </tr>
    <tr>
        <th colspan="1">R</th>
        <th colspan="1">从光标所在位置开始替换字符，按Esc结束</th>
    </tr>
    <tr>
        <th colspan="1">cw</th>
        <th colspan="1">从光标所在位置开始替换单词，按Esc结束</th>
    </tr>
    <tr>
        <th colspan="1">:%s/aaa/bbb/g</th>
        <th colspan="1">把文件中全部的aaa替换成bbb</th>
    </tr>
    <tr> <!-- 注释 -->
        <th rowspan="2"> 可视</th>
        <th colspan="1">v</th>
        <th colspan="1"> 把当前行的下一行接到当前行的尾部 </th>
    </tr>
    <tr>
        <th colspan="1">Ctrl+V</th>
        <th colspan="1">列操作</th>
    </tr>
    <tr> <!-- 注释 -->
        <th rowspan="5"> 退出</th>
        <th colspan="1">:w</th>
        <th colspan="1"> 保存 </th>
    </tr>
    <tr>
        <th colspan="1">:w!</th>
        <th colspan="1">强制保存</th>
    </tr>
    <tr>
        <th colspan="1">:wq | :x</th>
        <th colspan="1">保存退出</th>
    </tr>
    <tr>
        <th colspan="1">:q</th>
        <th colspan="1">退出</th>
    </tr>
    <tr>
        <th colspan="1">:q!</th>
        <th colspan="1">不保存，强制退出</th>
    </tr>
    <tr> <!-- 注释 -->
        <th rowspan="4"> 其他</th>
        <th colspan="1">J</th>
        <th colspan="1"> 把当前行的下一行接到当前行的尾部 </th>
    </tr>
    <tr>
        <th colspan="1">Ctrl+g</th>
        <th colspan="1">显示光标所在位置的行号和文件的总行数</th>
    </tr>
    <tr>
        <th colspan="1">.</th>
        <th colspan="1">重复执行上一次执行的vi命令</th>
    </tr>
    <tr>
        <th colspan="1">~</th>
        <th colspan="1">对光标当前所在的位置的字符进行大小写转换</th>
    </tr>
</table>
