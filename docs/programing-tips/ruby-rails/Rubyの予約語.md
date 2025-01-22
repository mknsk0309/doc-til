# Ruby の予約語

- 予約語はクラス名、変数名などに用いることはできない。
- ただし接頭辞 `$`, `@`, `@@` が先頭についたものは予約語とは見なされない。
- また、`def` の後やメソッド呼び出しのピリオドの後などメソッド名であるとはっきり分かる場所ではメソッド名として用いることができる。

## Ruby 3.1 時点での予約語

```txt
BEGIN    class    ensure   nil      self     when
END      def      false    not      super    while
alias    defined? for      or       then     yield
and      do       if       redo     true     __LINE__
begin    else     in       rescue   undef    __FILE__
break    elsif    module   retry    unless   __ENCODING__
case     end      next     return   until
```
