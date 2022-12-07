## 부록 D: 유용한 개발 도구
이 부록에서는 Rust 프로젝트가 제공하는 몇 가지 유용한 개발 도구에 대해 이야기합니다. 
자동 서식 지정, 경고 수정을 적용하는 빠른 방법, linter 및 IDE와의 통합에 대해 살펴보겠습니다.

### rustfmt로 자동 포맷하기
`Rustfmt` 도구는 커뮤니티 코드 스타일에 따라 코드 형식을 다시 지정합니다. 
많은 협업 프로젝트에서 Rust를 작성할 때 사용할 스타일에 대한 논쟁을 방지하기 위해 `rustfmt`를 사용합니다. 
모든 사람이 이 도구를 사용하여 코드 형식을 지정합니다.

`rustfmt`를 설치하려면 다음을 입력하십시오.
```$ rustup component add rustfmt```

이 명령은 Rust가 rustc와 cargo를 모두 제공하는 방식과 유사하게 rustfmt와 cargo-fmt를 제공합니다. 
Cargo 프로젝트를 포맷하려면 다음을 입력하십시오:

```$ cargo fmt```
이 명령을 실행하면 현재 크레이트의 모든 Rust 코드가 다시 포맷됩니다. 
이것은 코드 의미 체계가 아니라 코드 스타일만 변경해야 합니다. `rustfmt`에 대한 자세한 내용은 [해당 문서][rustfmt]를 참조하세요.

[rustfmt]: https://github.com/rust-lang/rustfmt

### 코드 수정rustfix
Rustfix 도구는 Rust 설치에 포함되어 있으며 원하는 문제일 가능성이 있는 문제를 수정하는 명확한 방법이 있는 컴파일러 경고를 자동으로 수정할 수 있습니다. 
이전에 컴파일러 경고를 본 적이 있을 것입니다. 예를 들어 다음 코드를 고려하십시오.

파일 이름: src/main.rs
```
fn do_something() {}

fn main() {
    for i in 0..100 {
        do_something();
    }
}
```
여기에서 우리는 `do_something`함수를 100번 호출했지만 `for`루프는 변수 `i`를 사용하지 않았습니다. 
Rust는 이에 대해 다음과 같이 경고합니다.
```
$ cargo build
   Compiling myprogram v0.1.0 (file:///projects/myprogram)
warning: unused variable: `i`
 --> src/main.rs:4:9
  |
4 |     for i in 0..100 {
  |         ^ help: consider using `_i` instead
  |
  = note: #[warn(unused_variables)] on by default

    Finished dev [unoptimized + debuginfo] target(s) in 0.50s
```

