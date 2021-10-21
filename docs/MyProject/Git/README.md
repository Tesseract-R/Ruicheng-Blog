# Git版本控制系统

# 存储结构

在目标文件夹下建立一个.versionManagement隐藏文件夹，用于存储所有的备份信息，目标文件夹下的所有文件和文件夹生成对应Blob/Tree模块保存在隐藏文件夹中。

- Key-value存储
  - value：Object的内容
  - Key：Object内容的hash
- Object的三种类型
  1. Blob：文件
     - Blob的Value：文件内容（不包含文件名）
     - Blob的Key：文件内容的hash值
  2. Tree：文件夹
     - Tree的Value：1.子文件夹和子文件名称；2.每个子文件Blob key；3.每个子文件夹tree的key；
     - Tree的Key：Tree的Value的hash值
  3. Commit：提交
     - Commit的Value：仓库tree对象的key、前驱commit对象的key、时间戳、备注
     - Commit的Key：Commit的Value的hash值

在branch文件夹中存储了当前所有的分支，每个文件的文件名为分支名，存储的内容为这个分支上最新一次提交的commitID。最后HEAD文件中存储了当前所在分支的名字。



# 功能的实现思路

- 提交

  对目标文件夹生成一次Hash值，对比与最新一次提交的Hash值是否相同。如果不同就进行一次提交，将目标文件夹的Hash值、上一次提交记录的commitID、提交时间以及备注写入文件，生成的commitID作为文件名，并且当前分支的文件记录下这次commitID。

- 查看提交记录

  输入：无

  输出：LinkedHashMap<commitID, 根目录Hash值>

  根据HEAD文件找到最新的一次commit记录，每次commit都记录了上一次的commit记录，便可以链表遍历寻找到这个分支上所有的commit记录。最后返回每一条commitID与对应commit的根目录Hash值以键值对的形式组成的LinkedHashMap。

  ```java
  /**
  * 以链表形式返回commit记录、对应的根结点hash值
  * @return
  * @throws Exception
  */
  public LinkedHashMap commitLog() throws Exception {
      LinkedHashMap result = new LinkedHashMap<String,String>();
      String commit_id = cmt.getLatestCommit();
      do {
          result.put(commit_id,cmt.getInfoOfHomeFolder(commit_id,"hashOfHomeFolder"));
          commit_id = cmt.getInfoOfHomeFolder(commit_id,"Parent");
      }while (!commit_id.equals("null"));
      return result;
  }
  ```

- 回滚

  输入：需要回退的commitID

  输出：回滚是否成功结果

  首先判断输入commitID是否在记录中存在，然后根据commitID在LinkedHashMap中寻找到对应的根目录Hash值。之后以递归的形式复原这次commit记录下的文件。最后修改当前分支记录的commitID。

  

  恢复文件的部分代码：

  - 根据tree的key查询得到value
  - 解析value中的每一条记录，即这个tree对象所代表的文件夹内的子文件与子文件夹名称以及对应的blob/tree key
  - 对于blob，在path中创建文件，命名为相应的文件名，写入blob的value
  - 对于tree，在path中创建文件夹，命名为相应的文件夹名，递归调用恢复(path+文件夹名)

  ```java
  /**
       * 递归恢复文件
       * @param filename
       * @param recursivePath
       * @throws Exception
       */
      private void rb(String filename, String recursivePath) throws Exception{
          String filenamePath = storagePath +"\\"+ filename;
          File treeNode = new File(filenamePath);
          InputStreamReader isr = new InputStreamReader(new FileInputStream(treeNode));
          BufferedReader br = new BufferedReader(isr);
          String line = br.readLine();
          while(line != null){
              String[] list = line.split(" {2}");
              if(list[0].equals("Blob")){
                  FileInputStream is = new FileInputStream(storagePath+"\\"+list[1]);
                  FileOutputStream os = new FileOutputStream(recursivePath+"\\"+list[2]);
                  byte[] buffer = new byte[1024];
                  int numRead = 0;
                  while (numRead != -1) {
                      numRead = is.read(buffer);
                      //缓冲区读入numRead数量的字符
                      if (numRead > 0)
                          os.write(buffer, 0, numRead);
                  }
                  is.close();
                  os.close();
              }
              else if(list[0].equals("Tree")){
                  File f = new File(recursivePath + "\\" + list[2]);
                  if (!f.exists())
                      f.mkdir();
                  rb(list[1], recursivePath + "\\" + list[2]);  // 递归去深度优先遍历所有的文件
              }
              line = br.readLine();
          }
      }
  ```

- 查看所有分支

  输入：无

  输出：所有的分支及当前所在分支

  遍历输出branch文件夹中的所有文件名，然后根据HEAD中存储的信息输出当前所在的分支名

  ```java
  /**
  * 输出所有分支，和当前分支名字
  * @throws IOException
  */
  protected void branchList() throws IOException {
      File[] files = new File(storagePath + "\\branch").listFiles();
      System.out.println("目前已有分支：");
      for (File f : files)
          System.out.println(f.getName());
      
      File HEADFile = new File(storagePath + "\\HEAD");
      InputStreamReader isr = new InputStreamReader(new FileInputStream(HEADFile));
      BufferedReader br = new BufferedReader(isr);
      String str = br.readLine();
      System.out.println("当前所在分支：" + str);
  }
  ```

- 切换分支

  输入：需要切换的分支名

  输出：切换是否成功的结果

  首先在branch文件夹中寻找是否存在需要切换的分支，如果存在，就在HEAD中修改信息

  ```java
  /**
  * 切换分支
  * @param branchName
  * @return
  * @throws IOException
  */
  public boolean checkoutBranch(String branchName) throws IOException {
      File[] files = new File(storagePath + "\\branch").listFiles();
      for (File f : files)
          if (f.getName().equals(branchName)){
              createHead(branchName);
              return true;
          }
      return false;
  }
  ```


-   Diff

    [思路](diff.md)

