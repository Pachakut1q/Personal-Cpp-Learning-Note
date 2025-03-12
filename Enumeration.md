```
enum Example //4bytes, if "enum Example : char" 1byte
{
  A=5,B,C //A=5,B=6,C=7  default:0,1,2...
}

int main()
{
  Example value = B; //value = 1
}
```
