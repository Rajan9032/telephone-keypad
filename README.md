# telephone-keypad
a javascript based telephone keypad
#Telephone keypad
Creating a telephone keypad using javascript
var button = document.querySelectorAll('button'),
    input = document.querySelector('input'),
    busy = true,
    hold,
    is_busy,
    delay = 1000,
    change = -1,
    click = null;
    for (var i = 0, len = button.length; i < len; ++i) {
    button[i].onmousedown = function(e) {
        var text = this.getAttribute('data-text').split(""),
            number = this.getAttribute('data-number');
        busy = true;
        clearTimeout(is_busy);
        if (click !== e.target) {
            busy = false;
        }
        if (change >= text.length - 1 || click !== e.target) {
            change = 0;
            click = e.target;
        } else {
            change = change + 1;
        }
        if (text[0] === '#') {
            input.value = input.value.slice(0, -1);
            hold = setTimeout(function() {
                input.value = "";
            }, delay);
            return;
        }
        hold = setTimeout(function() {
            input.value = input.value.slice(0, -1) + number;
        }, delay);
        input.value = busy ? input.value.slice(0, -1) + text[change] : input.value + text[change];
    };
    button[i].onmouseup = function(e) {
        clearTimeout(hold);
        busy = true;
        is_busy = setTimeout(function() {
            change = -1;
            busy = false;
            e.target = null;
        }, delay);
        // put caret at the end of text input
        input.focus();
        input.selectionStart = input.selectionEnd = input.value.length;
    };
}


<p>
  <input type="text">
</p>
<p>
  <button data-text=".,?!'&quot;1-()@/:_" data-number="1">1 <small>o_o</small></button>
  <button data-text="abc2" data-number="2">2 <small>abc</small></button>
  <button data-text="def3" data-number="3">3 <small>def</small></button>
</p>
<p>
  <button data-text="ghi4" data-number="4">4 <small>ghi</small></button>
  <button data-text="jkl5" data-number="5">5 <small>jkl</small></button>
  <button data-text="mno6" data-number="6">6 <small>mno</small></button>
</p>
<p>
  <button data-text="pqrs7" data-number="7">7 <small>pqrs</small></button>
  <button data-text="tuv8" data-number="8">8 <small>tuv</small></button>
  <button data-text="wxyz9" data-number="9">9 <small>wxyz</small></button>
</p>
<p>
  <button data-text=" " data-number="">* <small>__</small></button>
  <button data-text=" 0" data-number="0">0 <small>__</small></button>
  <button data-text=" #" data-number="#"># <small>__</small></button>
</p>
