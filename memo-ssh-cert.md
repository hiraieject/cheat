
# ssh/key

## keygen からの公開キーコピー  
クライアントがWindowsでも　Powershellから同じコマンドラインでいける

	<client>

	clientpc $ ssh-keygen
	clientpc $
	clientpc $ ls -l ~/.ssh/id_rsa*
	-rw------- 1 username group 1811  9月 13 13:25 /home/username/.ssh/id_rsa
	-rw-rw-r-- 1 username group  391  9月 13 13:26 /home/username/.ssh/id_rsa.pub
	clientpc $
	clientpc $ scp ~/.ssh/id_rsa.pub username@192.168.0.xx:~/tmp_id_rsa.pub
	
	<server>
	
	serverpc $ cat ~/tmp_id_rsa.pub >> ~/.ssh/authorized_keys
	
