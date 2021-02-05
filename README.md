# iOS-study
iOS 공부 내용 정리

## TableView
### in storyboard   
TableViewController.swift와 storyboard에서 TableViewController 연결 : class명을 파일명과 일치시킴   
Object에서 TableView, TableViewCell 가져와서 배치   

**cell의 사이즈 조정 (row size)**
- TableViewCell의 size inspector에서 row height 조절
- TableView의 size inspector에서도 row height 조절

**custom cell**   
Object에서 imageView, Label 등 가져와서 배치   

**auto layout 설정**   
각 UI컴포넌트마다 contraint 설정 (size, rate, spacing..)   

### in TableViewController   
TableViewController는 UITableViewDataSource, UITableViewDelegate 프로토콜을 추가로 따름   
-> UITableViewDataSource, UITableViewDelegate도 storyboard에서 tableView와 ViewController control해서 연결해줘야함   
   
1. 몇개의 셀을 띄우는지
2. 어떤 셀을 보여줄건지
3. 셀 클릭시 어떤 일이 일어날건지
   
**UITableViewDataSource가 요구하는 함수**   
```
// 셀 몇개   
override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
   return 0 // 보통 데이터의 개수 리턴
}

// 행마다 무슨 셀
override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
   // Fetch a cell of the appropriate type.
   let cell = tableView.dequeueReusableCell(withIdentifier: "cellTypeIdentifier", for: indexPath)

   // Configure the cell’s contents.
   cell.textLabel!.text = "Cell text"

   return cell
}
```
두번째 함수에서 withIdentifier은 스토리보드에서 cell의 attribute inspector에서 identifier이다.   
해당 셀을 상수로 선언했으면 위의 코드처럼 데이터를 채울 수 있다. 셀을 리턴한다.

**UITableViewDelegate가 요구하는 함수**
```
func tableView(_ tableView: UITableView,
                   didSelectRowAt indexPath: IndexPath){
        print(indexPath.row)
}
```
cell이 선택됐을때 수행되어야 하는 일들을 정의하는 함수이다.   
지금은 일단 셀이 선택되면 해당 셀의 row index를 콘솔에 출력하도록 했다.   

처음엔 뷰 컨드롤러 안에 리스트형식으로 데이터를 저장해두고 indexPath.row로 접근하여 셀에 표현한다.   
