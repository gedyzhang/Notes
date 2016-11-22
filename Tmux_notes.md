Tmux是一个非常方便的工具：
- 用于在一个终端窗口中运行多个终端会话；
- 还可以通过 Tmux 使终端会话运行于后台或是按需接入、断开会话，这个功能非常实用

###tmux分为三个部分：会话（Session）、窗口（Window）、面板（Pane）
###tmux的快捷键：
- 进入tmux
<pre><code>$ tmux</pre></code>
- 退出tmux
<pre><code>$ exit(或者ctrl + d)</pre></code>

###Pane相关快捷键
- 横向分屏
<pre><code>$ Ctrl-b %</code></pre>
- 纵向分屏
<pre><code>$ Ctrl-b “</code></pre>
- 选择面板
<pre><code>$ Ctrl-b 方向键</code></pre>
- 关闭当前面板
<pre><code>$ Ctrl-b x</code></pre>

###Window相关快捷键
- 创建新窗口
<pre><code>$ Ctrl-b c</code></pre>
- 关闭窗口
<pre><code>$ Ctrl-b &</code></pre>
- 列出所有窗口
<pre><code>$ Ctrl-b w</code></pre>
- 上个窗口/下个窗口
<pre><code>$ Ctrl-b p</code></pre>
<pre><code>$ Ctrl-b n</code></pre>
- 切换到某个窗口号
<pre><code>$ Ctrl-b 窗口号</code></pre>
- 重命名窗口
<pre><code>$ Ctrl-b ,</code></pre>

###Session相关快捷键
- 创建Session
<pre><code>$ tmux new -s session_name</code></pre>
- 在Session中创建一个新的Session
<pre><code>$ new -s session_name</code></pre>
- 进入指定Session
<pre><code>$ tmux attach -t session_name</code></pre>
- 列出所有会话
<pre><code>$ Ctrl-b s</code></pre>
 
