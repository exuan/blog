title: php 求最大公约数
date: 2016-03-20 13:10:20
categories: algorithm,gcd
tags: [algorithm,gcd]
---
## 最大公约数
>最大公约数（Greatest Common Divisor，简写为G.C.D.；或Highest Common Factor，简写为H.C.F.），指某几个整数共有约数中最大的一个。
[维基百科](https://zh.wikipedia.org/wiki/%E6%9C%80%E5%A4%A7%E5%85%AC%E5%9B%A0%E6%95%B8)
[百度百科](http://baike.baidu.com/view/47637.htm)

<!--more--> 

## 解法
-  列举法：各自列出约数，再找出最大的公约数。
- 素因数分解法：两数各作素因数分解，然后取出共有的项乘起来。
- 短除法
- 辗转相除法(欧几里德算法):常使用于直观上不容易判别公约数的场合。

## php实现

##### 1. gmp扩展的 [gmp_gcd](http://php.net/manual/zh/function.gmp-gcd.php)
```php
// 需要注意一下gmp_gcd生成的是一个GMP对象
$gcd = gmp_gcd('12', '6');
echo $gcd . PHP_EOL;
var_dump($gcd);

/*
6
class GMP#1 (1) {
  public $num =>
  string(1) "6"
}
*/
```

#### 2. 辗转相除法(照抄的)
```php
function gcd($m, $n) {
	if($m == 0 || $n == 0) {
		return abs(max(abs($m), abs($n)));
	}

	$r = $m % $n;
	return $r ? gcd($n, $r) : abs($n);
}
```
####  Stein 算法
```php
function gcd($m, $n) { 
	if($m == 0 || $n == 0) {
		return abs(max(abs($m), abs($n)));
	}
	if($m % 2 == 0 && $n % 2 == 0) {
		return 2 * gcd($m / 2, $n / 2);
	} elseif($m % 2 == 0) {
		return gcd($m / 2, $n);	
	} elseif($n % 2 == 0) {
		return gcd($m, $n / 2);
	} else {
		 return gcd(($m + $n) / 2, ($m - $n) / 2);
	}
}
```
