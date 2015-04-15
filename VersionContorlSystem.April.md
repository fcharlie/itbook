**版**本控制（Revision control）是维护工程蓝图的标准作法，能追踪工程蓝图从诞生一直到定案的过程。此外，版本控制也是一种软件工程技巧，藉此能在软件开发的过程中，确保由不同人所编辑的同一程式档案都得到同步。

如果没有版本控制软件，团队化的软件开发将是个巨大的灾难，而解决这一切的是版本控制系统，版本控制系统的意义在于使代码的变更变得可控。    


版本控制软件的历史可以追溯到上世纪70年代，最早是CA Software Change Manager( Harvest/CCC) ，这一版本系统是Santa Barbara CA为军方开发的。有趣的是很多软件都是从军方流出来的。    
从此开始，版本控制系统的种类越来越多：

**版本控制年谱**

<table>
  <caption><em>版本控制软件</em></caption>
    <tr>
      <td></td>
      <td>开源/免费</td>
      <td>私有软件</td>
      <td>主流</td>
   </tr>
   <tr>
      <td>本地</td>
      <td>SCCS (1972) RCS (1982) </td>
      <td>PVCS (1985) QVCS (1991)</td>
      <td>RCS</td>
   </tr>
   <tr>
      <td>集中式</td>
      <td>CVS (1986, 1990 in C) CVSNT (1998) QVCS Enterprise (1998) Subversion (2000)</td>
      <td>Software Change Manager (1970s) Panvalet (1970s) Endevor (1980s) DSEE (1984) Synergy (1990) ClearCase (1992) CMVC (1994) Visual SourceSafe (1994) Perforce (1995) StarTeam (1995) Integrity (2001) Surround SCM (2002) AccuRev SCM (2002) SourceAnywhere (2003) Vault (2003) Team Foundation Server (2005) Team Concert (2008)
</td>
      <td>Subversion</td>
   </tr>
   <tr>
      <td>分布式</td>
      <td>GNU arch (2001) Darcs (2002) DCVS (2002) ArX (2003) Monotone (2003) SVK (2003) Codeville (2005) Bazaar (2005) Git (2005) Mercurial (2005) Fossil (2007) Veracity (2010) 
</td>
      <td>TeamWare (1990s?) Code Co-op (1997) BitKeeper (1998) Plastic SCM (2006)</td>
      <td>Git</td>
   </tr>
</table>


版本控制系统种类繁多，流行版本控制系统一般是如下几种：   
+ BitKeeper       
+ 协作版本系統|CVS] (Concurrent Versions System)                   
+ Micorosoft Visual SourceSafe/Team Foundation Server/Visual Studio Online       
+ Perforce    
+ Rational ClearCase       
+ RCS（GNU Revision Control System）         
+ Serena Dimention      
+ Subversion    
+ SVK    
+ Git      
+ Monotone        
+ Bazaar (software)          
+ Mercurial         
+ SourceGear Vault          

历史往往会留下蛛丝马迹，或许我们能从中找到答案，集中式版本控制系统的迭代周期较长，而分布式的版本控制系统却更加活跃，企业需要稳定的保守的策略，而社区需要冒险精神。

很有趣的是2005年诞生了多款版本控制软件，如果我们翻阅历史可以发现，Linux和BitKeeper的决裂正是那个时候，有兴趣的可以看一看。   
开源中国翻译： [Git 10 周年之际，创始人 Linus Torvalds 访谈](http://www.oschina.net/translate/10-years-of-git-an-interview-with-git-creator-linus-torvalds?utm_source=tuicool)

支持分布式系统的人认为：
>在 DVCS 和集中式版本控制系统之间有三个关键差异。第一个差异是，DVCS 通过本地提交支持离线工作，这是由 DVCS 的操作方式决定的。这与集中式版本控制完全不同，集中式版本控制要求通过到中心服务器的连接执行所有操作。这种灵活性让开发人员在飞机上也能够像在办公室中一样轻松地工作，可以一次又一次地进行提交。
第二个差异是 DVCS 比集中式系统更灵活，因为 DVCS 支持许多不同类型的工作流，从传统的集中式工作流到纯粹的特殊工作流，再到特殊工作流和集中式工作流的组合。这种灵活性允许通过电子邮件、对等网络和开发团队喜欢的任何方式进行开发。
第三个差异是 DVCS 比集中式版本控制系统快得多，因为大多数操作在客户机上进行，速度非常快。另外，在需要进行推（push ）操作（与另一个节点通信）时，速度也更快，因为两个客户机机器上都有完整的元数据。速度差异相当显著，根据使用本地存储库还是网络存储库，DVCS 比 Subversion 快大约 3-10 倍。

IBM developerWorks： [分布式版本控制系统入门](http://www.ibm.com/developerworks/cn/aix/library/au-dist_ver_control/)

当然，从另一方面讲，集中式版本控制对于商业软件来说，代码是可控的，完整的仓库放在服务器上，并不是每个人都有完整的权限可以将所有代码拉取下来，修改或者是合并都显得小心翼翼。企业对此很乐意看到。  
人们很容易觉得集中式版本控制具有更强的掌控能力。
集中式版本控制系统大成者非Subversion莫属，而分布式版本控制系统目前几乎由git掌控天下。   
到目前为止，很难再出现一个集中式版本控制系统超越Subversion的，而Subversion内部实现却可以。

###Subversion实现
Subversion实际上是循规蹈矩的，所作的一切努力全部是为了取代CVS，在协议的设计上基本上是按照对应的IETF制定的标准。    
Subversion主要的传输协议有3类，本地的file 以及svn(svn+ssh)还有http(https)。
Subversion的SVN协议，遵循ABNF标准，ABNF 即*扩充巴科斯-瑙尔范式*：      
>扩充巴科斯-瑙尔范式（ABNF）是一种基于巴科斯-瑙尔范式（BNF）的元语言，但它有自己的语法和派生规则。ABNF的原动原则是描述一种作为双向通信协议的语言的形式系统。它是由第68号互联网标准（"STD 68"，大小写样式按照原文）定义的，也就是RFC 5234，经常用于互联网工程任务组（IETF）通信协议的定义语言。——维基百科
       
使用SVN协议一般是运行svnserver服务，svnserver监听3690端口，svn客户端将URL等信息依照ABNF规则将数据封装发送给服务器，服务器将数据解析,解析依照命令读取仓库信息，按照ABNF格式返回数据给客户端。
svn传输主要的命令有       
>+ commit     
>+ diff     
>+ get-locations    
>+ check-path
>+ update
>+ other.......

服务端根据不同的命令执行相应的动作，实际上和http协议的流程是一样的。   
这些命令有的只是详细的列出仓库指定的信息，或者获得仓库文件，有的会对仓库的修改，在设计svn服务器的时候可以据此对用户接入权限控制进行设定。    

更多的命令和技术细节可以参看svn协议文档:    
[http://svn.apache.org/repos/asf/subversion/trunk/subversion/libsvn_ra_svn/protocol](http://svn.apache.org/repos/asf/subversion/trunk/subversion/libsvn_ra_svn/protocol)    

Subversion的HTTP协议使用WebDAV。
  * RFC 2518  (WebDAV)
  * RFC 3253  (DeltaV)   
  
WebDAV是HTTP 1.1的扩展协议，但它一种复杂的难以解析的协议，所以完全支持WebDAV的服务器并不多，更遑论DeltaV。支持WebDAV的有IIS,Apache httpd。Nginx只部分支持WebDAV，编译参数--with-http_dav_module 而Github上有nginx模块，支持WebDAV的PROPFIND和OPTIONS方法：[nginx-dav-ext-module](https://github.com/arut/nginx-dav-ext-module)。  

WebDAV与Subversion结合使得问题变得较为复杂，使用其他服务器，比如Nginx,WebDAV的方法要额外实现。有人在Nginx右键列表曾经咨询过，支持SVN需要
> full WebDAV support          
> DeltaV support        
> SVN repo format support      

不过以Igor Sysoev的尿性，坚决不鸟。
SVN的URL或许带有特殊的关键字，这些对应特定的操作，关键字如下： 
>!svn/rvr            
>!svn/txr              
>!svn/me           
>!svn/bln            
>!svn/blah        
>!svn/vcc             
>!svn/bc          
>!svn/act     
>!svn/bc    
>!svn/wrk

对应的细节：
>Version Controlled Resource (VCC):                            !svn/vcc                  
>Baseline resource:                                                       !svn/bln               
>Working baseline resource:                                        !svn/wbl                
>Baseline collection resource:                                      !svn/bc/REV/                 
>Activity collection:                                                     !svn/act/ACTIVITY-UUID/               
>Versioned resource:                                                   !svn/ver/REV/path              
>Working resource:                                                      !svn/wrk/ACTIVITY-UUID/path              


           
比如!svn/rev就可以用来diff比较差异，比较差异后，服务端将diff添加到HTTP包体中，客户端解析xml文件后，再解析diff。
>Example       
>+++++++      
>        
>Request:          
>         
>  GET /repos/test/!svn/ver/3/httpd/configure HTTP/1.1         
>  X-SVN-VR-Base: /repos/test/!svn/ver/2/httpd/configure         
>  Accept-Encoding: svndiff1;q=0.9,svndiff;q=0.8           
>         
>Response:          
>            
>  HTTP/1.1 200 OK           
>  ETag: "3//httpd/configure"             
>  Vary: Accept-Encoding              
>  Content-Type: application/vnd.svn-svndiff             
 
 Subversion的HTTP协议使用WebDAV,一切都离不开xml，按照现在流行JSON的说法，这种老掉牙的XML解析起来非常麻烦，而且还浪费带宽，比如svn log:

<code>
log-report


Purpose: Retrieve the log <span class="hljs-keyword">for</span> a portion of the repository.

Target URL: Current baseline collection <span class="hljs-keyword">for</span> a directory plus relative paths.
            Example: REPORT /repos/test/!svn/bc/<span class="hljs-number">5</span>/httpd/support

Request:

  &lt;S:log-report xmlns:S=<span class="hljs-string">"svn:"</span>&gt;
    &lt;S:start-revision&gt;<span class="hljs-number">2</span>&lt;/S:start-revision&gt;
    &lt;S:end-revision&gt;<span class="hljs-number">2</span>&lt;/S:end-revision&gt;
    &lt;S:limit&gt;<span class="hljs-number">1</span>&lt;/S:limit&gt; (optional)
    &lt;S:discover-changed-paths/&gt; (optional)
    &lt;S:strict-node-history/&gt; (optional)
    &lt;S:include-merged-revisions/&gt; (optional)
    &lt;S:encode-binary-props&gt; (optional)
    &lt;S:revprop&gt;REVPROP&lt;/S:revprop&gt;<span class="hljs-keyword">...</span> | &lt;S:all-revprops/&gt; | &lt;S:no-revprops/&gt;
      (<span class="hljs-string">'revprop'</span>, <span class="hljs-string">'all-revprops'</span>, and <span class="hljs-string">'no-revprops'</span> are all optional)
    &lt;S:path&gt;&lt;/S:path&gt;<span class="hljs-keyword">...</span> (optional)
  &lt;/S:log-report&gt;

Response:

  &lt;?xml version=<span class="hljs-string">"1.0"</span> encoding=<span class="hljs-string">"utf-8"</span>?&gt;
  &lt;S:log-report xmlns:S=<span class="hljs-string">"svn:"</span> xmlns:D=<span class="hljs-string">"DAV:"</span>&gt;
    &lt;S:log-item&gt;
      &lt;D:version-name&gt;<span class="hljs-number">2</span>&lt;/D:version-name&gt;
      &lt;S:creator-displayname&gt;bob&lt;/S:creator-displayname&gt;
      &lt;S:date&gt;<span class="hljs-number">2006</span>-<span class="hljs-number">02</span>-27T18:<span class="hljs-number">44</span>:<span class="hljs-number">26.</span>149336Z&lt;/S:date&gt;
      &lt;D:comment&gt;Add doo-hickey&lt;/D:comment&gt;
      &lt;S:revprop name=<span class="hljs-string">"REVPROP"</span>&gt;value&lt;/S:revprop&gt;<span class="hljs-keyword">...</span> (optional)
      &lt;S:revprop name=<span class="hljs-string">"REVPROP"</span> encoding=<span class="hljs-string">"base64"</span>&gt;encoded value&lt;/S:revprop&gt;<span class="hljs-keyword">...</span> (optional)
      &lt;S:has-children/&gt; (optional)
      &lt;S:added-path( copyfrom-path=<span class="hljs-string">"PATH"</span> copyfrom-rev=<span class="hljs-string">"REVNUM"</span>&gt;PATH&lt;/S:added-path&gt;<span class="hljs-keyword">...</span> (optional)
      &lt;S:replaced-path( copyfrom-path=<span class="hljs-string">"PATH"</span> copyfrom-rev=<span class="hljs-string">"REVNUM"</span>&gt;PATH&lt;/S:replaced-path&gt;<span class="hljs-keyword">...</span> (optional)
      &lt;S:deleted-path&gt;PATH&lt;/S:deleted-path&gt;<span class="hljs-keyword">...</span> (optional)
      &lt;S:modified-path&gt;PATH&lt;/S:modified-path&gt;<span class="hljs-keyword">...</span> (optional)
    &lt;/S:log-item&gt;
    ...multiple log-items <span class="hljs-keyword">for</span> each returned revision...
  &lt;/S:log-report&gt;
</code>

按照我的尿性，我是不愿意去解析这些鬼的。如果使用JSON，解析起来要方便的多。
 
Subversion具体的WebDAV协议内容地址如下：
[http://svn.apache.org/repos/asf/subversion/trunk/notes/http-and-webdav/webdav-protocol](http://svn.apache.org/repos/asf/subversion/trunk/notes/http-and-webdav/webdav-protocol)

随着HTTP 2.0的发布，SVN开发者也开始思考移除WebDAV，使用HTTP 2.0完全取代WebDAV. 
HTTP 2.0路线计划：   
[http://svn.apache.org/repos/asf/subversion/trunk/notes/http-and-webdav/http-protocol-v2.txt](http://svn.apache.org/repos/asf/subversion/trunk/notes/http-and-webdav/http-protocol-v2.txt)

Subversion的布局
完整的检出一个Subversion仓库，在工作目录下执行tree命令，得到如下布局：  

![SubversionLayout][2]

![SubversionLayout2][3]

```
[url=]  
L      abc.c               # svn已经在.svn目录锁定了abc.c                
M      bar.c               # bar.c的内容已经在本地修改过了               
M      baz.c               # baz.c属性有修改，但没有内容修改            
X      3rd_party           # 这个目录是外部定义的一部分           
?      foo.o               # svn并没有管理foo.o              
!      some_dir            # svn管理这个，但它可能丢失或者不完整          
~      qux                 # 作为file/dir/link进行了版本控制，但类型已经改变             
I      .screenrc           # svn不管理这个，配置确定要忽略它           
A  +   moved_dir           # 包含历史的添加，历史记录了它的来历            
M  +   moved_dir/README    # 包含历史的添加，并有了本地修改            
D      stuff/fish.c        # 这个文件预定要删除            
A      stuff/loot/bloo.h   # 这个文件预定要添加            
C      stuff/loot/lump.c   # 这个文件在更新时发生冲突            
R      xyz.c               # 这个文件预定要被替换           
S      stuff/squawk        # 这个文件已经跳转到了分支              
```

Subversion 路线图：          
![svnroadmap][1]

###Git内幕
Git对文件较敏感，存在工作目录的文件都会被Git及时的发现，并且要求用户添加到暂存区
Git版本控制中目录不作为一个单独的对象被添加到仓库，工作目录下的目录至少得找到一个文件才会被纳入版本控制。

实际上来说，由于Git的特性，直接支持大文件是不切实际的，但办法不是没有，目前Github已经开源了一个git扩展 [git-lfs](https://github.com/github/git-lfs) 实现Git的大文件托管。

####从libgit2 看Git实现
如果要从源码去研究GIT是如何实现的，没有久经考验之前，我会选择libgit2，开源中国软件收录了libgit2: [http://www.oschina.net/p/libgit2/](http://www.oschina.net/p/libgit2/) 。

Git Object type 
>typedef enum {
>	GIT_OBJ_ANY = -2,		/**< Object can be any of the following */            
>	GIT_OBJ_BAD = -1,		/**< Object is invalid. */          
>	GIT_OBJ__EXT1 = 0,		/**< Reserved for future use. */           
>	GIT_OBJ_COMMIT = 1,		/**< A commit object. */       
>	GIT_OBJ_TREE = 2,		/**< A tree (directory listing) object. */           
>	GIT_OBJ_BLOB = 3,		/**< A file revision object. */         
>	GIT_OBJ_TAG = 4,		/**< An annotated tag object. */        
>	GIT_OBJ__EXT2 = 5,		/**< Reserved for future use. */        
>	GIT_OBJ_OFS_DELTA = 6, /**< A delta, base is given by an offset. */         
>	GIT_OBJ_REF_DELTA = 7, /**< A delta, base is given by object id. */          
>} git_otype;           

Git Ref type:    
>typedef enum {       
>	GIT_REF_INVALID = 0, /**< Invalid reference */       
>	GIT_REF_OID = 1, /**< A reference which points at an object id */            
>	GIT_REF_SYMBOLIC = 2, /**< A reference which points at another reference */             
>	GIT_REF_LISTALL = GIT_REF_OID|GIT_REF_SYMBOLIC,          
>} git_ref_t;          


Git Branch type:
>typedef enum {        
>	GIT_BRANCH_LOCAL = 1,       
>	GIT_BRANCH_REMOTE = 2,       
>	GIT_BRANCH_ALL = GIT_BRANCH_LOCAL|GIT_BRANCH_REMOTE,           
>} git_branch_t;           


比如说git_filemode_t ，这些都呵Unix的文件属性有关系。比如GIT_FILEMODE_BLOB_EXECUTABLE的值就是0100755，比如我们使用chmod命令可以将文件轻松的赋予可执行权限，这个值正好是755。
>$>chmod 755 hello.sh   
>等价 chmod +x hello.sh

从这些信息我们可以知道一些问题是如何出现的。
>无论是Github的Subversion 还是OSC@GIT的Subversion都无法避免的一个问题，无法提交空目录，在Git的概念里，目录是一个tree，如果这个tree无法向下遍历到任何一个文件，也就是blob，commit,link，那么这个目录就不会被纳入到版本控制里面去。

Git File mode type:

>typedef enum {          
>	GIT_FILEMODE_UNREADABLE          = 0000000,       
>	GIT_FILEMODE_TREE                = 0040000,        
>	GIT_FILEMODE_BLOB                = 0100644,        
>	GIT_FILEMODE_BLOB_EXECUTABLE     = 0100755,        
>	GIT_FILEMODE_LINK                = 0120000,     
>	GIT_FILEMODE_COMMIT              = 0160000,    
>} git_filemode_t;   


目前libgit2支持的安全协议有x509与ssh v2。      

>typedef enum git_cert_t {        
>	GIT_CERT_X509,      
>	GIT_CERT_HOSTKEY_LIBSSH2,       
>} git_cert_t;         

Git Submodule:

>typedef enum {       
>	GIT_SUBMODULE_UPDATE_RESET    = -1,           
>	GIT_SUBMODULE_UPDATE_CHECKOUT = 1,       
>	GIT_SUBMODULE_UPDATE_REBASE   = 2,       
>	GIT_SUBMODULE_UPDATE_MERGE    = 3,         
>	GIT_SUBMODULE_UPDATE_NONE     = 4,          
>  GIT_SUBMODULE_UPDATE_DEFAULT  = 0          
>} git_submodule_update_t;        


如果你要从一次commit拿到一个特定的文件，我会选择，先拿到commit id，然后找到root tree-entry的object id,从这个tree entry拿到指定path的tree-entry id,查看文件类型git_tree_entry_filemode_raw，如果是个blob,就使用git_blob_rawcontent查看文件内容。


事实上，也不要对libgit2抱有太高的期望，毕竟libgit2 1.0遥遥无期，而官方的git还在快速迭代，标准也在不断的调整。

###Subversion
Subversion经过多年的努力，基本上已经取代了CVS，在集中式版本控制领域完全没有敌手，然而危机却会透过密不透风的墙,最大的危机来自思想的巨变。

##后来
显然，目前的版本控制系统正慢慢的变革，比如Veracity就将Bug追踪作为关注点。

###终话：
不换轮子就换车

1.其他的版本控制系统可查看维基百科：   
[http://en.wikipedia.org/wiki/List_of_revision_control_software](http://en.wikipedia.org/wiki/List_of_revision_control_software)


  [1]: http://static.oschina.net/uploads/space/2015/0413/101740_iK4m_139664.png
  [2]: http://static.oschina.net/uploads/space/2015/0411/201730_NJem_139664.png
  [3]: http://upload.wikimedia.org/wikipedia/commons/thumb/a/af/Revision_controlled_project_visualization-2010-24-02.svg/220px-Revision_controlled_project_visualization-2010-24-02.svg.png