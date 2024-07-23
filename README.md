## :joystick:	Refactoring Changes

### `TalentDonationProjectService.java`

#### Original Code & Refactored Code
```java
 /*
 * Project 이름으로 검색 - 객체된 Project 반환하기
 * @param projectName 프로젝트 이름
 * @return TalentDonationProject 검색된 프로젝트
 */
public TalentDonationProject getDonationProject(String projectName) {

  //Original Code
  for (TalentDonationProject project : donationProjectList) {
    if (project != null && project.getTalentDonationProjectName().equals(projectName)) {
      return project; //메소드 자체의 종료
    }
  }
  return null;

  //Refactored Code
  return donationProjectList.stream()
      .filter(project -> project != null && project.getTalentDonationProjectName().equals(projectName))
      .findFirst()
      .orElse(null);
}
```

### `EndView.java`

#### Original Code & Refactored Code

```java
//진행중인 모든 프로젝트 출력
public static void projectListView(ArrayList<TalentDonationProject> allProbonoProject){
    int index = 1;
    for (TalentDonationProject project : allProbonoProject) {
        if (project != null) {
            System.out.println("[진행 중인 project : " + (index++) + "] " + project);
        }
    }
}

//Refactored Code
//진행중인 모든 프로젝트 출력
public static void projectListView(ArrayList<TalentDonationProject> allProbonoProject){
    AtomicInteger index = new AtomicInteger(1);
    allProbonoProject.stream()
        .filter(project -> project != null)
        .forEach(project -> System.out.println("[진행 중인 project : " + index.getAndIncrement() + "] " + project));
}



