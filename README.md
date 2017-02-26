# Airbnb Ruby Style Guide - Vietnamese (Tiếng Việt)

Status / Tình trạng : Processing /Chưa xong 

# Nội Dung 

Đây là toàn bộ bài viết được dịch từ [Airbnb's Ruby Style Guide](https://github.com/airbnb/ruby).

Bài viết này được lấy cảm hứng từ [Github's guide](https://web.archive.org/web/20160410033955/https://github.com/styleguide/ruby) và [Bozhidar Batsov's guide][bbatsov-ruby].

Airbnb cũng đang hỗ trợ cho một [JavaScript Style Guide][airbnb-javascript].

## Mục Lục
  1. [Khoảng trắng/ Khoảng cách](#whitespace)
    1. [Thụt đầu dòng](#indentation)
    1. [Trong cùng một dòng](#inline)
    1. [Dòng mới](#newlines)
  1. [Chiều dài của dòng](#line-length)
  1. [Chú thích](#commenting)
    1. [Chú thích cho File/class-level](#fileclass-level-comments)
    1. [Chú thích cho Function](#function-comments)
    1. [Chú thích trong block và trong dòng](#block-and-inline-comments)
    1. [Dấu chấm câu, lỗi chính tả và ngữ pháp](#punctuation-spelling-and-grammar)
    1. [Chú thích TODO](#todo-comments)
    1. [Commented-out code](#commented-out-code)
  1. [Các phương thức (Methods)](#methods)
    1. [Các phương thức định nghĩa (Method definitions)](#method-definitions)
    1. [Các cách gọi phương thức (Method calls)](#method-calls)
  1. [Biểu thức điều kiện (Conditional Expressions)](#conditional-expressions)
    1. [Từ khóa điều kiện (Conditional keywords)](#conditional-keywords)
    1. [Ternary operator](#ternary-operator)
  1. [Cú pháp (Syntax)](#syntax)
  1. [Naming](#naming)
  1. [Classes](#classes)
  1. [Exceptions](#exceptions)
  1. [Collections](#collections)
  1. [Strings](#strings)
  1. [Regular Expressions](#regular-expressions)
  1. [Percent Literals](#percent-literals)
  1. [Rails](#rails)
    1. [Scopes](#scopes)
  1. [Be Consistent](#be-consistent)
  1. [Translation](#translation)

## Khoảng trắng / Khoảng cách

### Thụt đầu dòng

* <a name="default-indentation"></a>Sử dụng phím tab với 2 khoảng trắng thụt vào<sup>[[link](#default-indentation)]</sup>

* <a name="indent-when-as-case"></a>Thụt đầu dòng cho `when` cùng cấp như `case`.
    <sup>[[link](#indent-when-as-case)]</sup>

    ```ruby
    case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration > 120
      puts 'Too long!'
    when Time.now.hour > 21
      puts "It's too late"
    else
      song.play
    end

    kind = case year
           when 1850..1889 then 'Blues'
           when 1890..1909 then 'Ragtime'
           when 1910..1929 then 'New Orleans Jazz'
           when 1930..1939 then 'Swing'
           when 1940..1950 then 'Bebop'
           else 'Jazz'
           end
    ```

* <a name="align-function-params"></a>Căng lề cho function parameters như trên cùng một hàng ngang hoặc hàng dọc <sup>[[link](#align-function-params)]</sup>

    ```ruby
    # bad
    def self.create_translation(phrase_id, phrase_key, target_locale,
                                value, user_id, do_xss_check, allow_verification)
      ...
    end

    # good
    def self.create_translation(phrase_id,
                                phrase_key,
                                target_locale,
                                value,
                                user_id,
                                do_xss_check,
                                allow_verification)
      ...
    end

    # good
    def self.create_translation(
      phrase_id,
      phrase_key,
      target_locale,
      value,
      user_id,
      do_xss_check,
      allow_verification
    )
      ...
    end
    ```

* <a name="indent-multi-line-bool"></a>Thọc đầu dòng cho các line tiếp theo   của cùng một biểu thức boolean<sup>[[link](#indent-multi-line-bool)]</sup>

    ```ruby
    # bad
    def is_eligible?(user)
      Trebuchet.current.launch?(ProgramEligibilityHelper::PROGRAM_TREBUCHET_FLAG) &&
      is_in_program?(user) &&
      program_not_expired
    end

    # good
    def is_eligible?(user)
      Trebuchet.current.launch?(ProgramEligibilityHelper::PROGRAM_TREBUCHET_FLAG) &&
        is_in_program?(user) &&
        program_not_expired
    end
    ```

### Trong cùng một dòng

* <a name="trailing-whitespace"></a>Không bao giờ có dấu khoảng cách/khoảng trắng (Never leave trailing whitespace).
    <sup>[[link](#trailing-whitespace)]</sup>

* <a name="space-before-comments"></a>Khi chú thích cho code của bạn trên cùng một dòng cần phai có dấu khoảng cách giữa code và chú thích của bạn.
    <sup>[[link](#space-before-comments)]</sup>

    ```ruby
    # bad
    result = func(a, b)# we might want to change b to c

    # good
    result = func(a, b) # we might want to change b to c
    ```

* <a name="spaces-operators"></a>Sử dụng các khoảng trắng trước và sau `operators`; sau dâu phẩy,
    dấu hai chấm, và dấu phẩy; trước và sau `{` cũng như `}`.
    <sup>[[link](#spaces-operators)]</sup>

    ```ruby
    sum = 1 + 2
    a, b = 1, 2
    1 > 2 ? true : false; puts 'Hi'
    [1, 2, 3].each { |e| puts e }
    ```

* <a name="no-space-before-commas"></a>Không bao giờ có khoảng cách trước dấu phẩy
    <sup>[[link](#no-space-before-commas)]</sup>

    ```ruby
    result = func(a, b)
    ```

* <a name="spaces-block-params"></a>Không nên có khoảng trắng trong block `parameter pipes`. Hoặc khoảng trắng giữa các `parameters` trong một `block`. Hoặc có thêm một khoảng trắng ở bên ngoài `block parameter pipes`.
    <sup>[[link](#spaces-block-params")]</sup>

    ```ruby
    # bad
    {}.each { | x,  y |puts x }

    # good
    {}.each { |x, y| puts x }
    ```

* <a name="no-space-after-!"></a>Không nên có khoảng trắng giữa `!` và `argument`<sup>[[link](#no-space-after-!)]</sup>

    ```ruby
    !something
    ```

* <a name="no-spaces-braces"></a>Không có khoảng trắng sau `(`, `[`  hoặc trước `]`, `)`.
    <sup>[[link](#no-spaces-braces)]</sup>

    ```ruby
    some(arg).other
    [1, 2, 3].length
    ```

* <a name="no-spaces-string-interpolation"></a>Không nên có khoảng trắng sau `{` hoặc trước `}` khi viết một biến trong một chuỗi(string)<sup>[[link](#no-spaces-string-interpolation)]</sup>

    ```ruby
    # bad
    var = "This #{ foobar } is interpolated."

    # good
    var = "This #{foobar} is interpolated."
    ```

* <a name="no-spaces-range-literals"></a>Không sử dụng các khoảng trống thừa trong range
    literals.<sup>[[link](#no-spaces-range-literals)]</sup>

    ```ruby
    # bad
    (0 ... coll).each do |item|

    # good
    (0...coll).each do |item|
    ```

### Dòng mới

* <a name="multiline-if-newline"></a>Nếu có nhiều điều kiện cho mệnh đề `if` thì nên chia ra thành nhiều dòng để giúp phân biệt rõ ràng hơn.
    <sup>[[link](#multiline-if-newline)]</sup>

    ```ruby
    if @reservation_alteration.checkin == @reservation.start_date &&
       @reservation_alteration.checkout == (@reservation.start_date + @reservation.nights)

      redirect_to_alteration @reservation_alteration
    end
    ```

* <a name="newline-after-conditional"></a>Thêm một dòng mới sau điều kiện, block, các trường hợp `case`<sup>[[link](#newline-after-conditional)]</sup>

    ```ruby
    if robot.is_awesome?
      send_robot_present
    end

    robot.add_trait(:human_like_intelligence)
    ```

* <a name="newline-different-indent"></a>Không nên có các dòng trống giữa các
    `indentation` khác nhau (như giữa `class` hoặc `module` với các method
    bên trong nó).
    <sup>[[link](#newline-different-indent)]</sup>

    ```ruby
    # bad
    class Foo

      def bar
        # body omitted
      end

    end

    # good
    class Foo
      def bar
        # body omitted
      end
    end
    ```

* <a name="newline-between-methods"></a>Nên chỉ có một dòng trống giữa các `method` với nhau<sup>[[link](#newline-between-methods)]</sup>

    ```ruby
    def a
    end

    def b
    end
    ```

* <a name="method-def-empty-lines"></a>Sử dụng một dòng trống duy nhất để phân biệt các logic cho từng bước.
    <sup>[[link](#method-def-empty-lines)]</sup>

    ```ruby
    def transformorize_car
      car = manufacture(options)
      t = transformer(robot, disguise)

      car.after_market_mod!
      t.transform(car)
      car.assign_cool_name!

      fleet.add(car)
      car
    end
    ```

* <a name="trailing-newline"></a>Cuối mỗi file nên chỉ có một dòng trống là đủ.
    <sup>[[link](#trailing-newline)]</sup>

## Chiều dài của dòng
* Độ dài của dòng code sao cho có thể dễ dàng đọc và hiểu được. Tốt nhất nên ít hơn 100 kí tự.
  ([lý do](./rationales.md#line-length))<sup>
  [[link](#line-length)]</sup>

## Chú thích
> Việc viết chú thích cho code là điều quan trọng và cần phải làm, điều đó sẽ giúp
> người khác dễ hiêu hơn. Đây là những qui tắc bạn cần chú thích và chú thích ở đâu.
> Nhưng bạn phải nhớ: chú thích là quan trọng, code tốt nhất như là có một tài liệu sẵn
> (the best code is self-documenting). Đặt tên các kiểu và biến dễ hiểu thì sẽ tốt hơn
> bạn phải chú thích thêm ở sau đó
> Khi bạn viết chú thích bạn hãy xem mình như một nhà viết sách, những người
> kế tiếp cần phải hiểu được code của bạn (Be generous — the next one may be you!)

&mdash;[Google C++ Style Guide][google-c++]

Các phần này được trích từ 
[C++][google-c++-comments] và [Python][google-python-comments] style guides.

### Chú thích cho File/class-level

Mỗi định nghĩa cho một `class` nên có những chú thich để mô tả nó làm những gì
và sử dụng nó như thế nào.

Một file có chứa nhiều `class` hay không có `class` nào cũng nên có chú thích
ở đầu của nó

```ruby
# Automatic conversion of one locale to another where it is possible, like
# American to British English.
module Translation
  # Class for converting between text between similar locales.
  # Right now only conversion between American English -> British, Canadian,
  # Australian, New Zealand variations is provided.
  class PrimAndProper
    def initialize
      @converters = { :en => { :"en-AU" => AmericanToAustralian.new,
                               :"en-CA" => AmericanToCanadian.new,
                               :"en-GB" => AmericanToBritish.new,
                               :"en-NZ" => AmericanToKiwi.new,
                             } }
    end

  ...

  # Applies transforms to American English that are common to
  # variants of all other English colonies.
  class AmericanToColonial
    ...
  end

  # Converts American to British English.
  # In addition to general Colonial English variations, changes "apartment"
  # to "flat".
  class AmericanToBritish < AmericanToColonial
    ...
  end
```

Các tập tin bao gồm dữ liệu và file config cũng nên có **file-level comments**

```ruby
# List of American-to-British spelling variants.
#
# This list is made with
# lib/tasks/list_american_to_british_spelling_variants.rake.
#
# It contains words with general spelling variation patterns:
#   [trave]led/lled, [real]ize/ise, [flav]or/our, [cent]er/re, plus
# and these extras:
#   learned/learnt, practices/practises, airplane/aeroplane, ...

sectarianizes: sectarianises
neutralization: neutralisation
...
```

### Chú thích cho Function

Mỗi `function` nên có chú thích ở trước để mô tả chức năng và cách sử dụng. 
Các chú thích mô tả cho `function`, nó cũng sẽ không nói function đó sẽ làm những gì.
Nhìn chung, các chú thích này không mô tả cách các chức năng thực hiện nhiệm vụ của mình.
Thay vào đó nên nên cho các chú thích xen kẽ giữa các dòng code.


Mỗi function nên đề cập đến đầu ra và đầu vào là những gì. 
Trừ khi nó đáp ứng tất cả các tiêu chí sau:

* Không thể nhìn thấy bên ngoài (not externally visible)
* rất ngắn (very short)
* rõ ràng (obvious)

Bạn có thể sử dụng bất cứ định dạng nào mà bạn muốn. Trong Ruby, 2 tài liệu phổ biến là [TomDoc](http://tomdoc.org/) và
[YARD](http://rubydoc.info/docs/yard/file/docs/GettingStarted.md). Bạn có thể viết những điều đó một cách súc tích nhất có thể:

```ruby
# Returns the fallback locales for the_locale.
# If opts[:exclude_default] is set, the default locale, which is otherwise
# always the last one in the returned list, will be excluded.
#
# For example:
#   fallbacks_for(:"pt-BR")
#     => [:"pt-BR", :pt, :en]
#   fallbacks_for(:"pt-BR", :exclude_default => true)
#     => [:"pt-BR", :pt]
def fallbacks_for(the_locale, opts = {})
  ...
end
```

### Chú thích trong Block và trong cùng một dòng

Là nơi có những chú thích cho những phần code phức tạp. Nếu bạn phải giải thích
và review code, bạn nên chú thích cho nó ngay bây giờ. Các code `operations` 
phức tạp nên có vài dòng chú thích trước khi bắt đầu. Những đoạn code không rõ ràng
cũng nên có chú thích ở cuối.


```ruby
def fallbacks_for(the_locale, opts = {})
  # dup() to produce an array that we can mutate.
  ret = @fallbacks[the_locale].dup

  # We make two assumptions here:
  # 1) There is only one default locale (that is, it has no less-specific
  #    children).
  # 2) The default locale is just a language. (Like :en, and not :"en-US".)
  if opts[:exclude_default] &&
      ret.last == default_locale &&
      ret.last != language_from_locale(the_locale)
    ret.pop
  end

  ret
end
```

Mặc khác, không bao giờ mô tả cho code. Giả sử người đọc code biết ngôn ngữ đó 
(mặc dù không phải những gì bạn cố găng làm) tốt hơn so với bạn làm.

<a name="no-block-comments"></a>Liên quan: không sử dụng một khối gồm nhiều chú thích
cho nhiều dòng code bởi vì nó thật sự khó quan sát<sup>[[link](#no-block-comments)]</sup>

  ```ruby
  # bad
  =begin
  comment line
  another comment line
  =end

  # good
  # comment line
  # another comment line
  ```

### Dấu chấm câu, lỗi chính tả và ngữ pháp

Hãy chú ý đến dấu chấm câu, lỗi chính tả và ngữ pháp, sẽ dễ dàng hơn nếu đọc hiểu tốt các chú thích của bạn. 

Các chú thích nên được viết như văn bản tường thuật, có ngắt nghỉ hợp lý. Trong nhiều trường, câu hoàn chỉnh dễ hiểu hơn so với một câu vắn tắt. 

Sử dụng dấu chấm phẩy hoặc dấu phẩy hợp lý. Việc đó rất quan trọng để duy trì tính rõ ràng và dễ đọc. Đúng dâu chấm, dấu phẩy và ngữ pháp sẽ giúp bạn diễn đạt vấn đề rõ ràng hơn.

### Chú thích cho TODO (Các việc cần làm)

Sử dụng chú thích cho TODO để thay thế các đoạn code khi chúng chưa được viết. Nó cần ngắn gọn và dễ hiểu nhưng không cần quá hoàn hảo.

TODOs should include the string TODO in all caps, followed by the full name
of the person who can best provide context about the problem referenced by the
TODO, in parentheses. A colon is optional. A comment explaining what there is
to do is required. The main purpose is to have a consistent TODO format that
can be searched to find the person who can provide more details upon request.
A TODO is not a commitment that the person referenced will fix the problem.
Thus when you create a TODO, it is almost always your name that is given.

```ruby
  # bad
  # TODO(RS): Use proper namespacing for this constant.

  # bad
  # TODO(drumm3rz4lyfe): Use proper namespacing for this constant.

  # good
  # TODO(Ringo Starr): Use proper namespacing for this constant.
```

### Commented-out code

* <a name="commented-code"></a>Never leave commented-out code in our codebase.
    <sup>[[link](#commented-code)]</sup>

## Các phương thức

### Các phương thức định nghĩa (Method definitions)

* <a name="method-def-parens"></a>Sử dụng `def` với dấu ngoặc đơn khi có 
    parameters. Bỏ qua không dùng ngoặc đươn khi không có parameters.<sup>[[link](#method-def-parens)]</sup>

     ```ruby
     def some_method
       # body omitted
     end

     def some_method_with_parameters(arg1, arg2)
       # body omitted
     end
     ```

* <a name="no-default-args"></a>Không sử dụng arguments mặc định. Thay vào đó hãy dùng các tùy chọn (options)<sup>[[link](#no-default-args)]</sup>

    ```ruby
    # bad
    def obliterate(things, gently = true, except = [], at = Time.now)
      ...
    end

    # good
    def obliterate(things, options = {})
      default_options = {
        :gently => true, # obliterate with soft-delete
        :except => [], # skip obliterating these things
        :at => Time.now, # don't obliterate them until later
      }
      options.reverse_merge!(default_options)

      ...
    end
    ```

* <a name="no-single-line-methods"></a>Tránh các single-line methods. Mặc dù nó cò phần phổ biến, có một vài đặc thù về định nghĩa làm cho việc sử dụng chúng không như mong muốn.
    <sup>[[link](#no-single-line-methods)]</sup>

    ```ruby
    # bad
    def too_much; something; something_else; end

    # good
    def some_method
      # body
    end
    ```

### Các cách gọi phương thức (Method calls)

**Sử dụng dấu ngoặc đơn** để gọi phương thức (method):

* <a name="returns-val-parens"></a>Nếu method trả về giá trị
    <sup>[[link](#returns-val-parens)]</sup>

    ```ruby
    # bad
    @current_user = User.find_by_id 1964192

    # good
    @current_user = User.find_by_id(1964192)
    ```

* <a name="first-arg-parens"></a>Nếu đối số đầu tiên của method được sử dụng<sup>[[link](#first-arg-parens)]</sup>

    ```ruby
    # bad
    put! (x + y) % len, value

    # good
    put!((x + y) % len, value)
    ```

* <a name="space-method-call"></a>Không bao giờ có khoảng cách / khoảng trắng giữa dâu ngoặc đơn và tên method<sup>[[link](#space-method-call)]</sup>

    ```ruby
    # bad
    f (3 + 2) + 1

    # good
    f(3 + 2) + 1
    ```

* <a name="no-args-parens"></a>**Không có dấu ngoặc đơn** cho method nếu nó không có đối số truyền vào<sup>[[link](#no-args-parens)]</sup>

    ```ruby
    # bad
    nil?()

    # good
    nil?
    ```

* <a name="no-return-parens"></a>Nếu method không trả về giá trị hay không quan trả về cái gì thì dấu ngoặc đơn cũng là một lựa chọn nếu có nhiều dòng, nhiều đối số truyền vào.
    <sup>[[link](#no-return-parens)]</sup>

    ```ruby
    # okay
    render(:partial => 'foo')

    # okay
    render :partial => 'foo'
    ```

Trong cả hai trường hợp:

* <a name="options-no-braces"></a>Nếu method chấp nhận đối số truyền vào cuối cùng là `hash`, không sử dụng `{` `}`.
    <sup>[[link](#options-no-braces)]</sup>

    ```ruby
    # bad
    get '/v1/reservations', { :id => 54875 }

    # good
    get '/v1/reservations', :id => 54875
    ```

## Biểu thức điều kiện

### Từ khóa điều kiện

* <a name="multiline-if-then"></a>Không bao giờ sử dụng `then` cho nhiều dòng `if/unless`.
    <sup>[[link](#multiline-if-then)]</sup>

    ```ruby
    # bad
    if some_condition then
      ...
    end

    # good
    if some_condition
      ...
    end
    ```

* <a name="multiline-while-until"></a>Không bao giờ sử dụng `do` cho nhiều dòng `while` hoặc
    `until`.<sup>[[link](#multiline-while-until)]</sup>

    ```ruby
    # bad
    while x > 5 do
      ...
    end

    until x > 5 do
      ...
    end

    # good
    while x > 5
      ...
    end

    until x > 5
      ...
    end
    ```

* <a name="no-and-or"></a>Các từ khóa `and`, `or`, và `not` đều không khả dungk. Nó chỉ là từ không có giá trị trong ruby. Thay vào đó luôn sử dụng `&&`, `||`, và `!`.
    <sup>[[link](#no-and-or)]</sup>

* <a name="only-simple-if-unless"></a>`if/unless` thì được chấp nhận khi nội dung đơn giản, điều kiện là đơn giản, và chỉ nằm trên một dòng. Nếu không hãy tránh `if/unless`.
    <sup>[[link](#only-simple-if-unless)]</sup>

    ```ruby
    # bad - this doesn't fit on one line
    add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page]) if request_opts[:trebuchet_experiments_on_page] && !request_opts[:trebuchet_experiments_on_page].empty?

    # okay
    if request_opts[:trebuchet_experiments_on_page] &&
         !request_opts[:trebuchet_experiments_on_page].empty?

      add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page])
    end

    # bad - this is complex and deserves multiple lines and a comment
    parts[i] = part.to_i(INTEGER_BASE) if !part.nil? && [0, 2, 3].include?(i)

    # okay
    return if reconciled?
    ```

* <a name="no-unless-with-else"></a>Không bao giờ sử dụng `unless` với `else`. <sup>[[link](#no-unless-with-else)]</sup>

    ```ruby
    # bad
    unless success?
      puts 'failure'
    else
      puts 'success'
    end

    # good
    if success?
      puts 'success'
    else
      puts 'failure'
    end
    ```

* <a name="unless-with-multiple-conditions"></a>Tránh dùng `unless` nhiều điều kiện<sup>[[link](#unless-with-multiple-conditions)]</sup>

    ```ruby
      # bad
      unless foo? && bar?
        ...
      end

      # okay
      if !(foo? && bar?)
        ...
      end
    ```

* <a name="parens-around-conditions"></a>Không sử dụng dấu ngoặc đơn xung quanh `if/unless/while`.
    <sup>[[link](#parens-around-conditions)]</sup>

    ```ruby
    # bad
    if (x > 10)
      ...
    end

    # good
    if x > 10
      ...
    end

    ```

### Ternary operator

* <a name="avoid-complex-ternary"></a>Avoid the ternary operator (`?:`) except
    in cases where all expressions are extremely trivial. However, do use the
    ternary operator(`?:`) over `if/then/else/end` constructs for single line
    conditionals.<sup>[[link](#avoid-complex-ternary)]</sup>

    ```ruby
    # bad
    result = if some_condition then something else something_else end

    # good
    result = some_condition ? something : something_else
    ```

* <a name="no-nested-ternaries"></a>Use one expression per branch in a ternary
    operator. This also means that ternary operators must not be nested. Prefer
    `if/else` constructs in these cases.<sup>[[link](#no-nested-ternaries)]</sup>

    ```ruby
    # bad
    some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

    # good
    if some_condition
      nested_condition ? nested_something : nested_something_else
    else
      something_else
    end
    ```

* <a name="single-condition-ternary"></a>Avoid multiple conditions in ternaries.
    Ternaries are best used with single conditions.
    <sup>[[link](#single-condition-ternary)]</sup>

* <a name="no-multiline-ternaries"></a>Avoid multi-line `?:` (the ternary
    operator), use `if/then/else/end` instead.
    <sup>[[link](#no-multiline-ternaries)]</sup>

    ```ruby
    # bad
    some_really_long_condition_that_might_make_you_want_to_split_lines ?
      something : something_else

    # good
    if some_really_long_condition_that_might_make_you_want_to_split_lines
      something
    else
      something_else
    end
    ```

## Cú pháp (Syntax)

* <a name="no-for"></a>Không bao giờ dùng `for`, trừ khi bạn biết chính xác lý do tại sao.
Hầu hết các vòng lặp thời gian nên được sử dụng thay thế. `for` thì thực giống như một phần của
    `each` (vì vật bạn đang thêm một cấp gián tiếp), nhưng với một twist - `for`
không giới hạn trong một phạm vi mới (không giôngd `each`) và các biến được định nghĩa trong nó
    block sẽ được hiển thị bên ngoài nó.<sup>[[link](#no-for)]</sup>

    ```ruby
    arr = [1, 2, 3]

    # bad
    for elem in arr do
      puts elem
    end

    # good
    arr.each { |elem| puts elem }
    ```

* <a name="single-line-blocks"></a>Prefer `{...}` tốt hơn `do...end` cho
    single-line blocks.  Tránh sử dụng `{...}` cho multi-line blocks (nhiều dòng thì không tốt cho lắm). Luôn dùng `do...end` cho "kiểm soát vòng lặp" và
    "định nghĩa phương thức".  Avoid `do...end`
    when chaining.<sup>[[link](#single-line-blocks)]</sup>

    ```ruby
    names = ["Bozhidar", "Steve", "Sarah"]

    # good
    names.each { |name| puts name }

    # bad
    names.each do |name| puts name end

    # good
    names.each do |name|
      puts name
      puts 'yay!'
    end

    # bad
    names.each { |name|
      puts name
      puts 'yay!'
    }

    # good
    names.select { |name| name.start_with?("S") }.map { |name| name.upcase }

    # bad
    names.select do |name|
      name.start_with?("S")
    end.map { |name| name.upcase }
    ```

    Một số cho rằng `multiline chaining` sẽ trông tốt hơn với việc dùng
    `{...}`, nhưng họ nên tự hỏi nếu chúng có thể thực sự đọc được và nội dung của `block` có thể được tách ra thành nhiều phương pháp tiện lợi.

* <a name="self-assignment"></a>Use shorthand self assignment operators
    whenever applicable.<sup>[[link](#self-assignment)]</sup>

    ```ruby
    # bad
    x = x + y
    x = x * y
    x = x**y
    x = x / y
    x = x || y
    x = x && y

    # good
    x += y
    x *= y
    x **= y
    x /= y
    x ||= y
    x &&= y
    ```

* <a name="semicolons"></a>Tránh dâu phẩy trong định nghĩa `single line class`. Không có khoảng trắng / khoảng cách trước dấu phẩy.<sup>[[link](#semicolons)]</sup>

    ```ruby
    # bad
    puts 'foobar'; # superfluous semicolon
    puts 'foo'; puts 'bar' # two expressions on the same line

    # good
    puts 'foobar'

    puts 'foo'
    puts 'bar'

    puts 'foo', 'bar' # this applies to puts in particular
    ```

* <a name="colon-use"></a>Sử dụng :: chỉ để tham khảo(bao gồm
    `classe` và `modules`) và `constructors` (giống như `Array()` hoặc `Nokogiri::HTML()`).
    Không dùng :: cho phương pháp gọi thông thường.<sup>[[link](#colon-use)]</sup>

    ```ruby
    # bad
    SomeClass::some_method
    some_object::some_method

    # good
    SomeClass.some_method
    some_object.some_method
    SomeModule::SomeClass::SOME_CONST
    SomeModule::SomeClass()
    ```

* <a name="redundant-return"></a>Tránh `return` khi không cần thiết.
    <sup>[[link](#redundant-return)]</sup>

    ```ruby
    # bad
    def some_method(some_arr)
      return some_arr.size
    end

    # good
    def some_method(some_arr)
      some_arr.size
    end
    ```

* <a name="assignment-in-conditionals"></a>Không sử dụng kết quả trả về của `=` trong
    câu điều kiện<sup>[[link](#assignment-in-conditionals)]</sup>

    ```ruby
    # bad - shows intended use of assignment
    if (v = array.grep(/foo/))
      ...
    end

    # bad
    if v = array.grep(/foo/)
      ...
    end

    # good
    v = array.grep(/foo/)
    if v
      ...
    end

    ```

* <a name="double-pipe-for-uninit"></a>Sử dụng `||=` để khởi tạo biến.
    <sup>[[link](#double-pipe-for-uninit)]</sup>

    ```ruby
    # set name to Bozhidar, only if it's nil or false
    name ||= 'Bozhidar'
    ```

* <a name="no-double-pipes-for-bools"></a>Không dùng `||=` để khởi tạo biến `boonlean`
. (Hãy xem xét những gì sẽ xảy ra nếu giá trị hiện tại đã xảy ra được
    `false`.)<sup>[[link](#no-double-pipes-for-bools)]</sup>

    ```ruby
    # bad - would set enabled to true even if it was false
    enabled ||= true

    # good
    enabled = true if enabled.nil?
    ```

* <a name="lambda-calls"></a>Sử dụng `.call` chính xác khi gọi lambdas.
    <sup>[[link](#lambda-calls)]</sup>

    ```ruby
    # bad
    lambda.(x, y)

    # good
    lambda.call(x, y)
    ```

* <a name="no-cryptic-perl"></a>Tránh dùng `Perl-style` các biến đặc biệt (giống như
    `$0-9`, `$`, ... ). Chúng thì khó hiểu và không khuyến khích sử dụng chúng trong bất kì trường hợp. Tên một biến dài nên giống như
    `$PROGRAM_NAME`.<sup>[[link](#no-cryptic-perl)]</sup>

* <a name="single-action-blocks"></a>Khi một `method block` chỉ có một đối số
    , và nội dung chỉ gồm đọc một thuộc tính hoặc gọi một phương thức không có đối số, sử dụng cách viết ngăn `&:`.
    <sup>[[link](#single-action-blocks)]</sup>

    ```ruby
    # bad
    bluths.map { |bluth| bluth.occupation }
    bluths.select { |bluth| bluth.blue_self? }

    # good
    bluths.map(&:occupation)
    bluths.select(&:blue_self?)
    ```

* <a name="redundant-self"></a>Prefer `some_method` tốt hơn `self.some_method` khi
    khi gọi một phương thức hiện tại.<sup>[[link](#redundant-self)]</sup>

    ```ruby
    # bad
    def end_date
      self.start_date + self.nights
    end

    # good
    def end_date
      start_date + nights
    end
    ```

   Trong ba trường hợp phố biến sau đây, `self.` là yêu cầu của ngôn ngữ
     và là tốt để sử dụng:

    1. Khi xác định một `class method`: `def self.some_method`.
    2. *left hand side* khi gọi một ssignment method, bao gồm cả thuộc tính khi `self` là một ActiveRecord model: `self.guest = user`.
    3. Referencing the current instance's class: `self.class`.

## Naming

* <a name="snake-case"></a>Use `snake_case` for methods and variables.
    <sup>[[link](#snake-case)]</sup>

* <a name="camel-case"></a>Use `CamelCase` for classes and modules. (Keep
    acronyms like HTTP, RFC, XML uppercase.)
    <sup>[[link](#camel-case)]</sup>

* <a name="screaming-snake-case"></a>Use `SCREAMING_SNAKE_CASE` for other
    constants.<sup>[[link](#screaming-snake-case)]</sup>

* <a name="predicate-method-names"></a>The names of predicate methods (methods
    that return a boolean value) should end in a question mark.
    (i.e. `Array#empty?`).<sup>[[link](#predicate-method-names)]</sup>

* <a name="bang-methods"></a>The names of potentially "dangerous" methods
    (i.e. methods that modify `self` or the arguments, `exit!`, etc.) should
    end with an exclamation mark. Bang methods should only exist if a non-bang
    method exists. ([More on this][ruby-naming-bang].)
    <sup>[[link](#bang-methods)]</sup>

* <a name="throwaway-variables"></a>Name throwaway variables `_`.
    <sup>[[link](#throwaway-variables)]</sup>

    ```ruby
    payment, _ = Payment.complete_paypal_payment!(params[:token],
                                                  native_currency,
                                                  created_at)
    ```

## Classes

* <a name="avoid-class-variables"></a>Avoid the usage of class (`@@`) variables
    due to their "nasty" behavior in inheritance.
    <sup>[[link](#avoid-class-variables)]</sup>

    ```ruby
    class Parent
      @@class_var = 'parent'

      def self.print_class_var
        puts @@class_var
      end
    end

    class Child < Parent
      @@class_var = 'child'
    end

    Parent.print_class_var # => will print "child"
    ```

  As you can see all the classes in a class hierarchy actually share one
  class variable. Class instance variables should usually be preferred
  over class variables.

* <a name="singleton-methods"></a>Use `def self.method` to define singleton
    methods. This makes the methods more resistant to refactoring changes.
    <sup>[[link](#singleton-methods)]</sup>

    ```ruby
    class TestClass
      # bad
      def TestClass.some_method
        ...
      end

      # good
      def self.some_other_method
        ...
      end
    ```
* <a name="no-class-self"></a>Avoid `class << self` except when necessary,
    e.g. single accessors and aliased attributes.
    <sup>[[link](#no-class-self)]</sup>

    ```ruby
    class TestClass
      # bad
      class << self
        def first_method
          ...
        end

        def second_method_etc
          ...
        end
      end

      # good
      class << self
        attr_accessor :per_page
        alias_method :nwo, :find_by_name_with_owner
      end

      def self.first_method
        ...
      end

      def self.second_method_etc
        ...
      end
    end
    ```

* <a name="access-modifiers"></a>Indent the `public`, `protected`, and
    `private` methods as much the method definitions they apply to. Leave one
    blank line above and below them.<sup>[[link](#access-modifiers)]</sup>

    ```ruby
    class SomeClass
      def public_method
        # ...
      end

      private

      def private_method
        # ...
      end
    end
    ```

## Exceptions

* <a name="exception-flow-control"></a>Don't use exceptions for flow of control.
    <sup>[[link](#exception-flow-control)]</sup>

    ```ruby
    # bad
    begin
      n / d
    rescue ZeroDivisionError
      puts "Cannot divide by 0!"
    end

    # good
    if d.zero?
      puts "Cannot divide by 0!"
    else
      n / d
    end
    ```

* <a name="dont-rescue-exception"></a>Avoid rescuing the `Exception` class.
    <sup>[[link](#dont-rescue-exception)]</sup>

    ```ruby
    # bad
    begin
      # an exception occurs here
    rescue Exception
      # exception handling
    end

    # good
    begin
      # an exception occurs here
    rescue StandardError
      # exception handling
    end

    # acceptable
    begin
      # an exception occurs here
    rescue
      # exception handling
    end
    ```

* <a name="redundant-exception"></a>Don't specify `RuntimeError` explicitly in
    the two argument version of raise. Prefer error sub-classes for clarity and
    explicit error creation.<sup>[[link](#redundant-exception)]</sup>

    ```ruby
    # bad
    raise RuntimeError, 'message'

    # better - RuntimeError is implicit here
    raise 'message'

    # best
    class MyExplicitError < RuntimeError; end
    raise MyExplicitError
    ```


* <a name="exception-class-messages"></a>
    Prefer supplying an exception class and a message as two separate arguments
    to `raise`, instead of an exception instance.
    <sup>[[link](#exception-class-messages)]</sup>

    ```Ruby
    # bad
    raise SomeException.new('message')
    # Note that there is no way to do `raise SomeException.new('message'), backtrace`.

    # good
    raise SomeException, 'message'
    # Consistent with `raise SomeException, 'message', backtrace`.
    ```


* <a name="rescue-as-modifier"></a>Avoid using rescue in its modifier form.
    <sup>[[link](#rescue-as-modifier)]</sup>

    ```ruby
    # bad
    read_file rescue handle_error($!)

    # good
    begin
      read_file
    rescue Errno:ENOENT => ex
      handle_error(ex)
    end
    ```

## Collections

* <a name="map-over-collect"></a>Prefer `map` over
    `collect`.<sup>[[link](#map-over-collect)]</sup>

* <a name="detect-over-find"></a>Prefer `detect` over `find`. The use of `find`
    is ambiguous with regard to ActiveRecord's `find` method - `detect` makes
    clear that you're working with a Ruby collection, not an AR object.
    <sup>[[link](#detect-over-find)]</sup>

* <a name="reduce-over-inject"></a>Prefer `reduce` over `inject`.
    <sup>[[link](#reduce-over-inject)]</sup>

* <a name="size-over-count"></a>Prefer `size` over either `length` or `count`
    for performance reasons.<sup>[[link](#size-over-count)]</sup>

* <a name="empty-collection-literals"></a>Prefer literal array and hash creation
    notation unless you need to pass parameters to their constructors.
    <sup>[[link](#empty-collection-literals)]</sup>

    ```ruby
    # bad
    arr = Array.new
    hash = Hash.new

    # good
    arr = []
    hash = {}

    # good because constructor requires parameters
    x = Hash.new { |h, k| h[k] = {} }
    ```

* <a name="array-join"></a>Favor `Array#join` over `Array#*` for clarity.
    <sup>[[link](#array-join)]</sup>

    ```ruby
    # bad
    %w(one two three) * ', '
    # => 'one, two, three'

    # good
    %w(one two three).join(', ')
    # => 'one, two, three'
    ```

* <a name="symbol-keys"></a>Use symbols instead of strings as hash keys.
    <sup>[[link](#symbol-keys)]</sup>

    ```ruby
    # bad
    hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

    # good
    hash = { :one => 1, :two => 2, :three => 3 }
    ```

* <a name="symbol-literals"></a>Relatedly, use plain symbols instead of string
    symbols when possible.<sup>[[link](#symbol-literals)]</sup>

    ```ruby
    # bad
    :"symbol"

    # good
    :symbol
    ```

* <a name="deprecated-hash-methods"></a>Use `Hash#key?` instead of
    `Hash#has_key?` and `Hash#value?` instead of `Hash#has_value?`. According
    to Matz, the longer forms are considered deprecated.
    <sup>[[link](#deprecated-hash-methods)]</sup>

    ```ruby
    # bad
    hash.has_key?(:test)
    hash.has_value?(value)

    # good
    hash.key?(:test)
    hash.value?(value)
    ```

* <a name="multiline-hashes"></a>Use multi-line hashes when it makes the code
    more readable, and use trailing commas to ensure that parameter changes
    don't cause extraneous diff lines when the logic has not otherwise changed.
    <sup>[[link](#multiline-hashes)]</sup>

    ```ruby
    hash = {
      :protocol => 'https',
      :only_path => false,
      :controller => :users,
      :action => :set_password,
      :redirect => @redirect_url,
      :secret => @secret,
    }
    ```

* <a name="array-trailing-comma"></a>Use a trailing comma in an `Array` that
    spans more than 1 line<sup>[[link](#array-trailing-comma)]</sup>

    ```ruby
    # good
    array = [1, 2, 3]

    # good
    array = [
      "car",
      "bear",
      "plane",
      "zoo",
    ]
    ```

## Strings

* <a name="string-interpolation"></a>Prefer string interpolation instead of
    string concatenation:<sup>[[link](#string-interpolation)]</sup>

    ```ruby
    # bad
    email_with_name = user.name + ' <' + user.email + '>'

    # good
    email_with_name = "#{user.name} <#{user.email}>"
    ```

  Furthermore, keep in mind Ruby 1.9-style interpolation. Let's say you are
  composing cache keys like this:

    ```ruby
    CACHE_KEY = '_store'

    cache.write(@user.id + CACHE_KEY)
    ```

    Prefer string interpolation instead of string concatenation:

    ```ruby
    CACHE_KEY = '%d_store'

    cache.write(CACHE_KEY % @user.id)
    ```

* <a name="string-concatenation"></a>Avoid using `String#+` when you need to
    construct large data chunks. Instead, use `String#<<`. Concatenation mutates
    the string instance in-place  and is always faster than `String#+`, which
    creates a bunch of new string objects.<sup>[[link](#string-concatenation)]</sup>

    ```ruby
    # good and also fast
    html = ''
    html << '<h1>Page title</h1>'

    paragraphs.each do |paragraph|
      html << "<p>#{paragraph}</p>"
    end
    ```

* <a name="multi-line-strings"></a>Use `\` at the end of the line instead of `+`
    or `<<` to concatenate multi-line strings.
    <sup>[[link](#multi-line-strings)]</sup>

    ```ruby
    # bad
    "Some string is really long and " +
      "spans multiple lines."

    "Some string is really long and " <<
      "spans multiple lines."

    # good
    "Some string is really long and " \
      "spans multiple lines."
    ```

## Regular Expressions

* <a name="regex-named-groups"></a>Avoid using `$1-9` as it can be hard to track
    what they contain. Named groups can be used instead.
    <sup>[[link](#regex-named-groups)]</sup>

    ```ruby
    # bad
    /(regexp)/ =~ string
    ...
    process $1

    # good
    /(?<meaningful_var>regexp)/ =~ string
    ...
    process meaningful_var
    ```

* <a name="caret-and-dollar-regexp"></a>Be careful with `^` and `$` as they
    match start/end of line, not string endings.  If you want to match the whole
    string use: `\A` and `\z`.<sup>[[link](#caret-and-dollar-regexp)]</sup>

    ```ruby
    string = "some injection\nusername"
    string[/^username$/]   # matches
    string[/\Ausername\z/] # don't match
    ```

* <a name="comment-regexes"></a>Use `x` modifier for complex regexps. This makes
    them more readable and you can add some useful comments. Just be careful as
    spaces are ignored.<sup>[[link](#comment-regexes)]</sup>

    ```ruby
    regexp = %r{
      start         # some text
      \s            # white space char
      (group)       # first group
      (?:alt1|alt2) # some alternation
      end
    }x
    ```

## Percent Literals

* <a name="percent-literal-delimiters"></a>Prefer parentheses over curly
    braces, brackets, or pipes when using `%`-literal delimiters for
    consistency, and because the behavior of `%`-literals is closer to method
    calls than the alternatives.<sup>[[link](#percent-literal-delimiters)]</sup>

    ```ruby
    # bad
    %w[date locale]
    %w{date locale}
    %w|date locale|

    # good
    %w(date locale)
    ```

* <a name="percent-w"></a>Use `%w` freely.<sup>[[link](#percent-w)]</sup>

    ```ruby
    STATES = %w(draft open closed)
    ```

* <a name="percent-parens"></a>Use `%()` for single-line strings which require
    both interpolation and embedded double-quotes. For multi-line strings,
    prefer heredocs.<sup>[[link](#percent-parens)]</sup>

    ```ruby
    # bad - no interpolation needed
    %(<div class="text">Some text</div>)
    # should be '<div class="text">Some text</div>'

    # bad - no double-quotes
    %(This is #{quality} style)
    # should be "This is #{quality} style"

    # bad - multiple lines
    %(<div>\n<span class="big">#{exclamation}</span>\n</div>)
    # should be a heredoc.

    # good - requires interpolation, has quotes, single line
    %(<tr><td class="name">#{name}</td>)
    ```

* <a name="percent-r"></a>Use `%r` only for regular expressions matching *more
    than* one '/' character.<sup>[[link](#percent-r)]</sup>

    ```ruby
    # bad
    %r(\s+)

    # still bad
    %r(^/(.*)$)
    # should be /^\/(.*)$/

    # good
    %r(^/blog/2011/(.*)$)
    ```

* <a name="percent-x"></a>Avoid the use of %x unless you're going to invoke a
    command with backquotes in it (which is rather unlikely).
    <sup>[[link](#percent-x)]</sup>

    ```ruby
    # bad
    date = %x(date)

    # good
    date = `date`
    echo = %x(echo `date`)
    ```

## Rails

* <a name="next-line-return"></a>When immediately returning after calling
    `render` or `redirect_to`, put `return` on the next line, not the same line.
    <sup>[[link](#next-line-return)]</sup>

    ```ruby
    # bad
    render :text => 'Howdy' and return

    # good
    render :text => 'Howdy'
    return

    # still bad
    render :text => 'Howdy' and return if foo.present?

    # good
    if foo.present?
      render :text => 'Howdy'
      return
    end
    ```

### Scopes
* <a name="scope-lambda"></a>When defining ActiveRecord model scopes, wrap the
    relation in a `lambda`.  A naked relation forces a database connection to be
    established at class load time (instance startup).
    <sup>[[link](#scope-lambda)]</sup>

    ```ruby
    # bad
    scope :foo, where(:bar => 1)

    # good
    scope :foo, -> { where(:bar => 1) }
    ```

## Be Consistent

> If you're editing code, take a few minutes to look at the code around you and
> determine its style. If they use spaces around all their arithmetic
> operators, you should too. If their comments have little boxes of hash marks
> around them, make your comments have little boxes of hash marks around them
> too.

> The point of having style guidelines is to have a common vocabulary of coding
> so people can concentrate on what you're saying rather than on how you're
> saying it. We present global style rules here so people know the vocabulary,
> but local style is also important. If code you add to a file looks
> drastically different from the existing code around it, it throws readers out
> of their rhythm when they go to read it. Avoid this.

&mdash;[Google C++ Style Guide][google-c++]

[airbnb-javascript]: https://github.com/airbnb/javascript
[bbatsov-ruby]: https://github.com/bbatsov/ruby-style-guide
[github-ruby]: https://github.com/styleguide/ruby
[google-c++]: https://google.github.io/styleguide/cppguide.html
[google-c++-comments]: https://google.github.io/styleguide/cppguide.html#Comments
[google-python-comments]: https://google.github.io/styleguide/pyguide.html#Comments
[ruby-naming-bang]: http://dablog.rubypal.com/2007/8/15/bang-methods-or-danger-will-rubyist

## Translation

  This style guide is also available in other languages:

  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [1c7/ruby-airbnb](https://github.com/1c7/ruby-airbnb)
