## ǰ��

* ���Ŵ����ʹ��git�����Ŷӿ����Ĺ����У��ܻ����һЩ�������Ҫȥ�ϲ���֧�Ĳ�������Ҳ�ᾭ�����������������Ϊ�Ͼ��������������ǻ��в�ͬ����ʱ������������һ����֧�Ͻ���ܶ����⣬��ʱ���Ǿ���Ҫ�����½���֧���в����ԵĿ��������ȷ�������ʱ���ٺϲ����������ύ������������

* ʹ��git���кϲ���֧˵��Ҳ���ѣ���Ϊ��ʹ��һ���Ǽ���������ѣ����ǲ�С�Ĳ����ܻ���һЩ����Ԥ�ϵ�������֣�������ƪ�ĵ��ͽ���һ����ô��git���кϲ���֧������

* ���˵һ�£�����ĵ��ǻ���[��ƪӢ���ĵ�](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)Ȼ�󼯺����Լ�������������ͨ��СС��ʵ�ʰ�����д�ģ�������Щ�������ĵط��������Ķ�ԭ�ģ�

## ��ʼ

�������������и�git�ֿ⣬�������ڹ�����master��֧�ϣ����Ǽ���һ���ļ�index.html���������£�

```html
<!DOCTYPE html>
<html>
<head>
	<title>git branch merging demo</title>
</head>
<body>

</body>
</html>
```

Ȼ�������½�һ����֧��Ȼ����index.html����һЩ�����Ե��޸ģ��������£�

```bash
   git checkout -b issue53
```

��������Ľ���ڵ�ǰmaster��֧�Ļ������½�һ����֧issue53Ȼ���л���issue53��֧����ʱissue53��masterָ�붼ָ��ͬһ�����ݣ���ͼ��ʾ��

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_1.png)

�����index.html�Ķ����£�

```html
	<!DOCTYPE html>
	<html>
	<head>
		<!--issue modifie-->
		<meta charset="utf-8"/>
		<title>git branch merging demo</title>
	</head>
	<body>

	</body>
	</html>
```

ok�������������ĸĶ�֮�����ڼ�����Ŀ����˵���ǵ�index.html�е����⼱���޸ģ�����������Ҫ�ص�master��֧���п������������ǵ�issue53��ô���أ���Ϊ������Ĺ����ǲ����ԵĿ���������ȷ���ܷ�ϲ���master�ϣ�������ֻ�ܵ����ύissue53��֧��Ȼ��ص�master��֧���������£�

```bash
	git commit -a -m 'initial issue53 branch'
	git checkout master
```

ok���������ڷ��ص�master��֧�������鿴������ָ֧��ָ���������ͼ��ʾ��

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_2.png)

��Ϊ��ʱ������master��֧�Ϸ�����bug��һ����������Ƕ�����master��֧�Ļ������½�һ���޸�bug�ķ�֧����bugȷ���޸���֮���ٺϲ���master��֧�ϣ����ǣ������½�һ����֧hotfix���������£�

```bash
	git checkout -b hotfix
```

��ʱ����html�Ķ����£�

```html
	<!DOCTYPE html>
	<!--hotfix modifie-->
	<html lang="Zh-cn">
	<head>
		<title>git branch merging demo</title>
	</head>
	<body>

	</body>
	</html>
```

Ȼ�������ύ���ֿ⣬�������£�

```bash
	git commit -a -m 'bug fixed'
```

�����ʱ�������������¸�����ָ֧��ָ�������

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_3.png)

����������ʱ�򣬿���ȷ�������������޸�����ȷ�ģ���ô����Ҫ��hotfix��֧�ϵ��޸ĺϲ���master��֧�ϣ�
�������£�

```bash
	git checkout master
	git merge hotfix
```

���Կ�������̨������£�

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_4.png)

�������ǿ���һ������Fast-forward��ʲô����»������������أ��������Ǵ���������ķ�֧������һ����֧����������һ����֧����ʷ�汾���ҵ�����ô�ͻ����Fast-forward��˵���˾�������һ����֧������һ����֧���ӷ�֧������ԭ�ĸ����Ľ��ͣ�

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_5.png)

��������������ºϲ���gitֻ�ǻ�򵥵ĸı�һ��master��ָ֧���ָ����ѣ�����ָ��������֧�����µİ汾����ʱ������ָ֧���ָ�����£�

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_6.png)

����һ�������ǾͿ���ɾ��hotfix��֧�ˣ���Ϊ�����Ѿ�����Ҫhotfix��֧�ˣ��������£�

```bash
	 git branch -d hotfix
```

�����ǵ�bug�޸����֮�����Ǿ���Ҫ�ص��ղ��жϿ����ķ�֧�ϣ�Ҳ����issue53��֧�ϣ��������£�

```bash
	git checkout issue53
```

������issue53��֧�϶�index.html�Ķ����£�

```html
<!DOCTYPE html>
<html>
<head>
	<!--issue modifie-->
	<meta http-equiv="content-type" content="text/html;charset=utf-8"/>
	<title>git branch merging demo</title>
</head>
<body>

</body>
</html>
```

����������һ�·�ָ֧��ָ�������

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_7.png)

�ã����ʱ�򣬼�����Ŀ���������issue53��֧�Ͻ��еĲ����Կ������Է�������ʽ�汾�ϣ��������Ǿ���Ҫ�ϲ�issue53��֧��master��֧�ϣ��������£�

```bash
	git checkout master
	git merge issue53
```

ok�����ǿ�һ���ն���������

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_8.png)

���ǿ��Կ����Ѿ�û��Fast-forward�����ˣ���ôgit����ô���кϲ����أ����� �ȿ�һ��ԭ������ô���������ģ�


![](https://github.com/woai30231/webDevDetails/blob/master/image/13_9.png)

��һ�仰�����;��ǣ�git������������ĺϲ���һ����ֱ��ҵ�������Ҫ�ϲ���֧�ĵ����ȣ�Ҳ����˵���ҵ�������ͬ�Ĳ��֣�Ȼ���ٷֱ���������ͬ�ķ�֧��������������ͬ�Ĳ��ֽ��кϲ����������һ����֧��Ҳ�����������պϲ��õ���master��֧����ʱ����������һ�·�ָ֧��ָ�������

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_10.png)

���ǿ��Կ�����ǰmaster��֧�ĸ��汾��������֧����Ϊ�����������������֣�

����һ�����ǲ�����Ϊ�ϲ���֧�ǲ��Ǻܼ��أ���Ȼ�����ˣ���������������ӷ�֧�ϸ�����ͬһ�������ݣ���ô���ǽ��кϲ���ʱ��ͻ���ֳ�ͻ��Ϊ����ʾ������⣬����������master��֧�Ļ����Ͻ���������֧dev1��dev2��ͬʱ�޸�ͬһ�������ݣ����»����ʲô������������£�

```bash
	git checkout -b dev1
	git checkout master
	git checkout -b dev2
```

��dev2��֧�ϸĶ����£�

```html
<!DOCTYPE html>
<!--hotfix modifie-->
<html lang="Zh-cn">
<head>
	<!--issue modifie-->
	<meta http-equiv="content-type" content="text/html;charset=utf-8"/>
	<title>git branch merging demo</title>
</head>
<body>
<div>dev2</div>
</body>
</html>
```

Ȼ���л���dev1��֧���������£�

```bash
  git checkout dev1
```

�Ķ����£�

```html
<!DOCTYPE html>
<!--hotfix modifie-->
<html lang="Zh-cn">
<head>
	<!--issue modifie-->
	<meta http-equiv="content-type" content="text/html;charset=utf-8"/>
	<title>git branch merging demo</title>
</head>
<body>
<div>dev1</div>
</body>
</html>
```
���Ǵ�ʱ��dev1��dev2��֧�ϸ�����master��֧��ͬһ�������ݣ������Ⱥϲ�dev1��֧��master���ٺϲ�dev2��֧��master��֧�������ʲô��ʾ���������£�

```bash
	git checkout master
	git merge dev1
	git merge dev2
```

�ն˽�ͼ���£�

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_11.png)

���ǿ��Կ����г�ͻ�ˣ�����ʾ��ͻ����index.html���������Ǵ�index.html��������ôһ�����ݣ���ͼ���£�

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_12.png)

������ʾ�������ںϲ���ʱ����ڳ�ͻ�ĵط������Ǹ�����Ҫ���ĳ��Լ���Ҫ������Ȼ�����ύ���ɣ����ʱ�����

```bash
	git status
```
�鿴���״̬��

�����ǰѳ�ͻ������֮�󣬾Ϳ���ʹ����������ɹ��ϲ��ˣ�

```bash
	git add .
	git commit -m 'submit'
```
��������ٲ鿴һ�½����

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_13.png)

### ���ݲ���

* ������Ϊ�е������ȳ��ˣ������в��ָ�д������û���ü����������������������������������д�����ݣ���϶������ʣ�gitʲôʱ��ϲ�������֧��ʱ�����ֳ�ͻ�أ����ҵľ���������������ںϲ���֧��ʱ���������������������϶�����ֳ�ͻ��1���ϲ���������֧����������������ϵ��Ҳ����˵a��֧������b��֧�ġ��ӡ���֧��˵���ˣ�����һ����ָ֧������ݲ���������һ����֧��ʷ�汾�е�һ����֧������ͼ��master��ָ֧�����hotfix��issue53��֧����һ���ύ�������������ǿ�������master��֧��hotfix��issue53�ġ��ӡ���֧����Ϊ��ָ�����ݶ�������hotfix��issue53����ʷ�ύ�汾���ҵ���2�����ںϲ���������֧�ϸ���ͬһ�������ݡ������������������������ô�ϲ���֧��ʱ��ض��������ͻ��

![](https://github.com/woai30231/webDevDetails/blob/master/image/13_3.png)

* ��ʵ��������ǾͿ���֪����������ƽʱ�����Ĺ����У�������¹��ܻ���bug�޸������ǲ�Ӧ��������֧���޸ģ�����Ӧ���½�һ����֧���ȹ�������֮�����bug�޸�֮���ٺϲ���ȥ�������Ͳ�����ֳ�ͻ�ˣ���Ϊ���ϲ����Ǹ���֧ʼ���ǡ��ӡ���֧�����ܱ�֤����֧�ĸɾ��ȶ���


