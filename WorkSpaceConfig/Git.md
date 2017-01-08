#Git & Git Hub
0. 安装git 

   $sudo apt-get install git
   $git --global config user.name $USERNAME
   $git --global config user.email $EMAIL

1. 生成秘钥并且将公钥加入到GitHub的个人配置文件中

   $ssh-keygen

2. 使用GitHub仓储的 "Clone with SSH"
   不要使用https的方式进行拉取，这样就可以不用使用密码来登录Github
