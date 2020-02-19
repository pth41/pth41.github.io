---
title:  "ARCore for Unity"
search: true
categories: 
  - AR
tags:
  - arcore
  - unity
last_modified_at: 2020-02-18T21:55:00-05:00
toc: true
---

**Unity를 사용해서 ARCore를 시작해보는 방법과 기능들을 알아보자** 

## 개발 환경 준비
- 무료버전 유니티 다운로드 [Unity](https://store.unity.com/kr/download?ref=personal)  

<img src="/assets/images/arcore/1.JPG" width="500px" height="400px" title="Terms" alt="Terms">  

- ARCore SDK for Unity 다운로드 [ARCore SDK for Unity](https://github.com/google-ar/arcore-unity-sdk/releases)

## ARCore를 사용할 프로젝트 생성  
새로운 유니티 프로젝트 생성  
  
<img src="/assets/images/arcore/2.JPG" width="600px" height="500px" title="Create_Project" alt="Create_Project">  
  
<br>
- 다운받은 ARCore sdk unitypackage를 실행하여 Import  

<img src="/assets/images/arcore/2.1.jpg" width="400px" height="300px" title="SDK_Import" alt="SDK_Import">  
  
<br>
- 안드로이드로 빌드셋
  - File메뉴 -> Build Settings (Ctrl+Shift+B)
  - 안드로이드 선택 후 Switch Platform
- 플레이어 세팅  

<img src="/assets/images/arcore/2.2.jpg" width="500px" height="400px" title="BuildSettings" alt="BuildSettings">  
  
<br>
## PlayerSettings 설정
- Other Settings 열기
- Multithreaded Rendering Off
- Package Name 정하기
- Minimum, Target API 7.0 ‘Nougat’ 이상  
  
<img src="/assets/images/arcore/3.JPG" width="400px" height="300px" title="PlayerSettings1" alt="PlayerSettings1">  
  
<br>
- XR Settings에서 ARCore Supported 체크  
  
<img src="/assets/images/arcore/4.JPG" width="400px" height="300px" title="PlayerSettings2" alt="PlayerSettings2">  
  
<br>
## 그 외
- Edit메뉴
  - Preferences
- SDK, JDK, NDK설정

<img src="/assets/images/arcore/edit.png" width="300px" height="200px" title="Edit" alt="Edit">  
  
<br>
<img src="/assets/images/arcore/sjn.png" width="550px" height="450px" title="SJN" alt="SJN">  
  
<br>

## HelloAR 샘플 앱
프로젝트가 준비되었으니 샘플 앱을 실행해보자
- Assets > GoogleARCore > Examples > HelloAR > Scenes > HelloAR 열기  

<img src="/assets/images/arcore/rud.JPG" width="500px" height="400px" title="Open_HelloAR" alt="Open_HelloAR">  
<br>
- Add Open Scenes
- Build And Run  

<img src="/assets/images/arcore/build.jpg" width="500px" height="400px" title="Build_HelloAR" alt="Build_HelloAR">  
  
<br>
테스트 할 수 있는 환경이면 Build and Run
아니라면 Build하여 생성된 apk파일을 디바이스로 옮겨 실행

<img src="/assets/images/arcore/run1.jpg" width="250px" height="150px" title="Run_HelloAR1" alt="Run_HelloAR1"> 
<img src="/assets/images/arcore/run2.jpg" width="250px" height="150px" title="Run_HelloAR2" alt="Run_HelloAR2">  
<br>
처음 실행시키면 카메라를 통해 평면을 찾는다  

<img src="/assets/images/arcore/run3.jpg" width="250px" height="150px" title="Run_HelloAR3" alt="Run_HelloAR3"> 
<img src="/assets/images/arcore/run4.jpg" width="250px" height="150px" title="Run_HelloAR4" alt="Run_HelloAR4">  
<br>
평면위에 터치를 하면 해당 위치에 Andy가 생성
생성된 객체는 카메라를 움직여도 그 자리에 고정  

<img src="/assets/images/arcore/run5.jpg" width="250px" height="150px" title="Run_HelloAR5" alt="Run_HelloAR5"> 
<img src="/assets/images/arcore/run6.jpg" width="250px" height="150px" title="Run_HelloAR6" alt="Run_HelloAR6">  
<br>
현실 조명에 따라 Andy의 셰이더가 반응

## Unity ARcore 사용
이제 직접 ARcore를 사용한다면 어떤 기능을 쓸 수 있는지 알아보자

- ARCore Device(AR 카메라) Prefab을 scene에 배치
  - 폰 뒷면에 있는 카메라를 사용하여 실제 이미지를 캡처하고 
    AR장면의 배경으로 사용할 수 있는 First Person Camera 게임 오브젝트를 보유
- Tracked Pose Driver -> scene 카메라와 전화기의 카메라(움직임)을 동기화
- Environmental Light prefab을 scene에 배치
  - ARCore의 주변 밝기 데이터에 ARCore 셰이더가 액세스 가능  

<img src="/assets/images/arcore/ard.png" width="400px" height="300px" title="ard" alt="ard">  
  
<br>

<img src="/assets/images/arcore/fpc.png" width="400px" height="300px" title="fpc" alt="fpc">  
  
<br>

<img src="/assets/images/arcore/5.JPG" width="400px" height="300px" title="prefab" alt="prefab">  
  
<br>
## Environmental Light 사용
- Environmental Light 배치
  - AR장면의 밝기을 조정하는 Prefab
- 모델 Matreial의 Shader를 DiffuseWithLightEstimation로 설정  

<img src="/assets/images/arcore/le.png" width="600px" height="500px" title="le" alt="le">  
  
<br>
## Motion Tracking
- 모션 트래킹 기능은 ARCore Device에 탑재
- 휴대전화가 세계에서 이동할 때 현실세계에 관련된 위치를 파악하는 것
- 캡처된 카메라 이미지에서 형상 포인트를 정하고 감지하여 위치 변화를 계산

<img src="/assets/images/arcore/mt.jpg" width="550px" height="450px" title="motion_tracking" alt="motion_tracking">  
  
<br>
## 모션 트래킹 확인
- HelloARController 스크립트 코드 참조 
  - `Update()` 메소드 각 프레임에서 중요작업 처리
- 세션은 ARCore의 카메라 프레임에 대한 정보를 보유
- 코드는 현재 세션의 TrackingState가 실제로 추적 중인지 테스트
  추적 중이지 않으면 화면 제한시간을 15초로 설정
  종료하기 전에 추적 상태를 복구
- Motion tracking 기능은 평면 감지 기능을 제공

```java
  // 모션 추적이 추적 중인지 확인합니다.
  if (Session.Status != SessionStatus.Tracking)
  {
      const int lostTrackingSleepTimeout = 15;
      Screen.sleepTimeout = lostTrackingSleepTimeout;
      if (!m_IsQuitting && Session.Status.IsValid())
      {
          SearchingForPlaneUI.SetActive(true);
      }

      return;
  }
```

## 실제 세계에서 새 planes 및 기존 planes 감지

- ARCore는 실제 세계에서 추적할 새 planes를 찾음  
  평면은 일반적인 표면에 있는 것으로 보이는 점의 군집

- 발견된 각 평면에 대해 새 게임 오브젝트가 생성되어 해당 평면을 시각화하고 추적

- 새 평면 및 기존 평면이 아직 감지되지 않는 한 "Seaching for Planes" UI텍스트 요소가 표시  
  하나 이상의 평면을 추적하면 텍스트 요소가 숨겨집니다.

```java
  // 이 프레임에서 발견된 평면을 반복하고 해당 GameObjects를 인스턴스화하여 시각화
  Session.GetTrackables<TrackedPlane>(m_NewPlanes, TrackableQueryFilter.New);
  for (int i = 0; i < m_NewPlanes.Count; i++)
  {
      // 평면 시각화 prefab을 인스턴스화하고 새 평면을 추적하도록 설정합니다. 변환이 다음처럼 설정
      // Unity World에서 Prefab의 mesh 이후 identity rotation의 원점이 업데이트
      // 좌표를 맞춤
      GameObject planeObject = Instantiate(TrackedPlanePrefab, Vector3.zero, Quaternion.identity,
          transform);
      planeObject.GetComponent<TrackedPlaneVisualizer>().Initialize(m_NewPlanes[i]);
  }

  // 유효한 평면이 없으면 snackbarUI를 사용하지 않음
  Session.GetTrackables<TrackedPlane>(m_AllPlanes);
  bool showSearchingUI = true;
  for (int i = 0; i < m_AllPlanes.Count; i++)
  {
      if (m_AllPlanes[i].TrackingState == TrackingState.Tracking)
      {
          showSearchingUI = false;
          break;
      }
  }

  SearchingForPlaneUI.SetActive(showSearchingUI);
```

## 가상 개체 배치를 위한 사용자 입력 처리

`Update()`메서드는 `planes` 들이 추적되고 시각화된 후에 AndyAndroid개체를 평면에 배치하기 위한 사용자 입력을 처리

- 사용자가 화면을 탭 할 때, `Frame.Raycast()`는 탭 위치에서 `raycast`를 사용해 사용자가 `planes` 또는 `oriented points`을 탭 했는지 여부를 감지

- 사용자가 `planes` 또는 `oriented points`의 표면을 누르면 사용자가 누른 위치에 있는 `TrackableHit pose`에서 AndyAndroid개체가 인스턴스화

- `hit pose`는 `Anchor`를 생성하는데 사용
	- `Anchor`는 Andy 게임 개체를 실제 세계와 비교해 같은 위치에 유지시켜줌  
	- 더 이상 `Anchor`가 필요하지 않은 경우 Unity의 GameObject인 `Destroy()`메서드를 호출  
	  이 신호는 ARCore가 `Anchor` 추적을 중지하라는 것 

- 이 카메라 위치는 Andy가 자신의 위치에서 카메라를 보는 것처럼 보이도록 Andy 객체의 `transform`을 조정하는 데 사용 

- Andy 객체의 변환은 `hit`의 `Anchor`를 상속하므로 `Anchor` 객체는 사용자가 전화기를 이동할 때 사용자가 놓은 위치에 유지 

```java
// Raycast는 플레이어가 평면을 검색하기 위해 터치한 위치와 대비 
// TrackableHit - ARCore에서 추적한 물리적 개체에 대한 Raycast히트에 대한 정보를 포함 
  TrackableHit hit;
  TrackableHitFlags raycastFilter = TrackableHitFlags.PlaneWithinPolygon  
      TrackableHitFlags.FeaturePointWithSurfaceNormal;

  if (Frame.Raycast(touch.position.x, touch.position.y, raycastFilter, out hit))
  {
      var andyObject = Instantiate(AndyAndroidPrefab, hit.Pose.position, hit.Pose.rotation);

      // ARCore가 물리적 환경에 대한 이해가 진화함에 따라 hitpoint를 추적할 수 있도록 anchor를 작성
      var anchor = hit.Trackable.CreateAnchor(hit.Pose);

      // 앤디는 카메라를 봐야 하지만 여전히 평면과 같은 수평에 있음
      if ((hit.Flags & TrackableHitFlags.PlaneWithinPolygon) != TrackableHitFlags.None)
      {
          // 카메라 위치를 잡고 y성분을 hit position와 일치
          Vector3 cameraPositionSameY = FirstPersonCamera.transform.position;
          cameraPositionSameY.y = hit.Pose.position.y;

          // Have Andy look toward the camera respecting his "up" perspective, which may be from ceiling.
          andyObject.transform.LookAt(cameraPositionSameY, andyObject.transform.up);
      }

      // Make Andy model a child of the anchor.
      andyObject.transform.parent = anchor.transform;
  }
```
