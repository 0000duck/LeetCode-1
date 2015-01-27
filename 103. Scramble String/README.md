�����ַ��� s1, s2, ���Ƿ��� scramble. --> ��������Ľ�Ϊ��`S(s1, s2)`, s1,s2 �ĳ���Ϊ n (�����ȣ�ֱ�� `return false;`).

Ȼ�󿴸��������ӣ�

	     gr|eat               rg|tae          ----- i == 2 (1)
	     /    \               /    \
	   g|r   e|at           r|g   ta|e        ----- i == 1 (2)
	   / \   / \            / \    / \
	  g   r e   a|t        r   g t|a  e       ----- i == 1 (3)
	            / \              / \
	           a   t            t   a

�����������������澿���м��������������ͼ��ʾ�Ĳ�����з�����

1. `S(s1, s2) = S(s1.substr(0,i), s2.substr(0,i)) && S(s1.substr(i), s2.substr(i))` (��һ�ֿ���)
2. �ص㿴 `e|at` �� `ta|e`, �����Ƶ�: `S(s1, s2) = S(s1.substr(0,i), s2.substr(n-i)) && S(s1.substr(i), s2.substr(0, n-i))` (�ڶ��ֿ���)
3. ���Բ��� 2. �����Կ��� S ��򵥵Ľ�: `S("a", "a") == true` �Լ� `S("t", "t") == true`. �� `if (s1 == s2) return true;`

�������������Եõ��ݹ�Ĺ�ʽ��

                 _________ true; 
     S(s1, s2) _|s1 == s2
                |      __ S(s1.substr(0,i), s2.substr(0,i)) && S(s1.substr(i), s2.substr(i))
                |_ or |
                      |__ S(s1.substr(0,i), s2.substr(n-i)) && S(s1.substr(i), s2.substr(n-i))


��Ȼ i �ķ�Χ�� [1 ,n-1]. 

-----

���������ʽ��֧�ţ����ǻ��������˵ݹ�ĳ��Ρ�Ҳ���������������д�����롣

```cpp

if (s1.empty() || s2.empty() || s1.size() != s2.size()) return false;

else if (s1 == s2) return true;


for (size_t i=1; i<s1.size(); ++i)

     if (isScramble(s1.substr(0,i), s2.substr(0,i)) && isScramble(s1.substr(i), s2.substr(i))) return true;

     else if (isScramble(s1.substr(0,i), s2.substr(s2.size()-i)) && isScramble(s1.substr(i), s2.substr(0, s2.size()-i))) return true;

return false;

```

���д�������Ѿ����߼��Ͻ��������⡣�����ȥ LeetCode ���ύ���ᷢ�� TimeOut. ��Ϊ������ʵ��ö�����졣����������ַ���������ͬ�������ַ�����ʵ�����˷�ʱ�䡣

�������ǿ����ų����������

1. s1 �� s2 ���ַ�����в��죬�� s1 ���� 'g', s2 ��ȴ�ޡ�ֱ�� `return false;`
2. s1 �� s2 ���ַ����ֵĸ����в��죬�� s1 �� 'g' �������Σ��� s2 ��ȴֻ��һ�Ρ�ֱ�� `return false;`.

���������������������ڵ����в�����룺

```cpp
for(auto c : s1)

     if (s2.find_first_of(c) == string::npos) return false;

     else if (std::count(s1.cbegin(), s1.cend(), c) != std::count(s2.cbegin(), s2.cend(), c)) return false;

```

Ȼ���ύ��AC, 16ms. ����˳�������
