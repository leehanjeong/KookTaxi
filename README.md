# [모바일 프로그래밍] Project_KookTaxi
### 국민대 소프트웨어학부 
## 20191604백연선 / 20191650이한정 / 20191670조나영 / 20191686최혜원
### https://github.com/Hyewon0223/KookTaxi
---
### 설명


- 목적지가 국민대인 사람들을 모아 택시를 함께 탈 수 있도록 하는 앱입니다.
- 동승하고 싶은 사람의 성별 여부, 인원수, 출발 지점(길음역, 광화문역, 홍대입구역, 동대문역사문화공원역) 등에 따라 사람들을 매칭해준다.
---
### 개발 환경
- Window OS
- Android Studio 4.1.1 (AVD: Pixel 2 API 30 / 안드로이드 폰)
---
### 사용 기술
- xml
- Java
- Firebase
<div>
    <img src="https://user-images.githubusercontent.com/55418359/99450379-0d355700-2964-11eb-9fe4-c4183249f090.JPG" width="200">
    <img src="https://user-images.githubusercontent.com/55418359/99450386-0e668400-2964-11eb-86d9-01762b75efb5.JPG" width="200">
</div>

- Google Cloud Platform(Maps SDK for Android API)
<div>
    <img src="https://user-images.githubusercontent.com/55418359/99349262-e41eb300-28de-11eb-8bd4-0cb2368d9b30.JPG" width="200">
    <img src="https://user-images.githubusercontent.com/55418359/99349264-e54fe000-28de-11eb-8448-44150c172a0d.JPG" width="200">
    <img src="https://user-images.githubusercontent.com/55418359/99349265-e5e87680-28de-11eb-80e5-358142a3bca6.JPG" width="200">
</div>

---
### 프로젝트 구성
* **다섯개의 액티비티**
  * **LoginActivity** - 로그인을 통해 MainActivity로 연결해주고, 회원이 아닐 시 JoinActivity로 연결해주는 액티비티
  * **JoinActivity** - 회원가입을 하는 액티비티
  * **MainActivity** - GPS기반으로 지도를 띄우고 서비스를 제공하는 역의 마커를 표시, 마커를 누르면 해당 역의 SearchActivity로 연결해주는 액티비티
  * **SearchActivity** - 본인이 탑승을 원하는 시간대의 방을 개설하거나 이미 있는 방에 들어가게 해주는 액티비티. ChatActivity로 연결해줌
  * **ChatActivity** - 사용자들끼리 채팅을 나눌 수 있도록 구현, 해당 어플의 원하는 대부분의 기능 동작을 위한 액티비티

* **여덟개의 xml**
  * **layout**
    * **activity_login.xml**
    * **activity_join.xml**
    * **activity_main.xml**
    * **activity_search.xml**
    * **activity_chat.xml**
    * **toolbar.xml**
  * **menu**
    * **menu1.xml**
    * **menu_toolbar.xml**
---
### 팀 내 역할
- 프로젝트를 기획하여 팀장 역할을 맡음
- MainActivity, ChatActivity, activity_main.xml, activity_chat.xml, menu1.xml를 담당함
---
### 실행 화면
<div>
    <img src="https://user-images.githubusercontent.com/55418359/99452281-b1200200-2966-11eb-96ea-0192e7beb21c.jpg" width="180">
    <img src="https://user-images.githubusercontent.com/55418359/99452288-b2512f00-2966-11eb-923c-83b82fc37abf.jpg" width="180">
    <img src="https://user-images.githubusercontent.com/55418359/99452289-b2e9c580-2966-11eb-9136-fec9ec33d89a.jpg" width="180">
    <img src="https://user-images.githubusercontent.com/55418359/99452292-b3825c00-2966-11eb-9f01-fbe6168c44da.jpg" width="180">
    <img src="https://user-images.githubusercontent.com/54920378/99683690-f86fd500-2ac3-11eb-87f0-1c796ebb53b8.jpg" width="180">
</div>

---
### 코드 관련 설명
#### manifests
* AndroidManifest.xml
  * 사용자의 위치 정보 접근을 위한 액세스 권한 
~~~xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
~~~
#### xml
* activity_main.xml
  * 기본 레이아웃은 RelativeLayout
  * map component 추가를 위한 Frame Layout 사용
<div>
  <img src="https://user-images.githubusercontent.com/54920378/99691191-4b4d8a80-2acc-11eb-9327-c3021f76e521.PNG" width="415">
  <img src="https://user-images.githubusercontent.com/54920378/99691196-4be62100-2acc-11eb-8f24-a3d7625142d9.PNG" width="200">
</div>

~~~xml
<FrameLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/container">

    <fragment
        android:id="@+id/map"
        android:name="com.google.android.gms.maps.SupportMapFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MapsActivity" />

</FrameLayout>
~~~
  
* activity_chat.xml
  * 기본 레이아웃은 LinearLayout
  * 채팅이 표시되는 부분은 ListView로 구현
  * 각종 View들을 이용하여 필요한 레이아웃 생성
<div>
  <img src="https://user-images.githubusercontent.com/54920378/99692850-18a49180-2ace-11eb-8bdb-16f5ce5c67b1.PNG" width="415">
  <img src="https://user-images.githubusercontent.com/54920378/99692854-193d2800-2ace-11eb-9be3-e2d1c2a3cac1.PNG" width="200">
</div>

~~~xml
<ListView
    android:id="@+id/lv_chating"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_marginBottom="100dp"></ListView>
    
<CheckedTextView
    android:id="@+id/checkedTextView1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginStart="5dp"
    android:layout_marginLeft="5dp"
    android:checkMark="?android:attr/listChoiceIndicatorMultiple"
    android:checked="false"
    android:text="사용자1" />
<EditText
    android:id="@+id/et_send"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:layout_weight="1"
    android:privateImeOptions="defaultInputmode=korean" />
~~~

* menu1.xml
  * menu - item 구조로 옵션 메뉴를 생성
  * group의 checkableBehavior를 이용하여 체크 기능을 이용하려 하였으나, 체크가 되지 않아(이유를 찾지 못함) 이용하지 못함. 아직 강퇴하기 메뉴에는 남아있음. 
<div>
    <img src="https://user-images.githubusercontent.com/54920378/99696826-776c0a00-2ad2-11eb-96a4-4392bdee931c.PNG" width="230">
</div>

**방장의 경우**
<div>
    <img src="https://user-images.githubusercontent.com/54920378/99698153-c9615f80-2ad3-11eb-806d-4d9246415963.PNG" width="220">
    <img src="https://user-images.githubusercontent.com/54920378/99696819-75a24680-2ad2-11eb-9727-14f25ac02c69.PNG" width="230">
    <img src="https://user-images.githubusercontent.com/54920378/99696820-75a24680-2ad2-11eb-8029-60862e0b1e55.PNG" width="235">
    <img src="https://user-images.githubusercontent.com/54920378/99696821-763add00-2ad2-11eb-9072-d85f17fd17d7.PNG" width="232">
</div>

**사용자의 경우**
<div>
    <img src="https://user-images.githubusercontent.com/54920378/99697853-74254e00-2ad3-11eb-8058-9862849a4b5b.PNG" width="255">
    <img src="https://user-images.githubusercontent.com/54920378/99697851-738cb780-2ad3-11eb-9c42-8788fb7b5d34.PNG" width="230">
</div>

#### Java
##### MainActivity.java, CharActivity.java
- 로그인의 조건이 모두 만족하면 Main 페이지로 이동 및 사용자의 정보(mail) 전달
~~~java
firebaseAuth.signInWithEmailAndPassword(mail,pw).addOnCompleteListener(LoginActivity.this, new OnCompleteListener<AuthResult>() {
    @Override
    public void onComplete(@NonNull Task<AuthResult> task) {
        if (task.isSuccessful()){
            Intent intent = new Intent(LoginActivity.this, MainActivity.class);
            intent.putExtra("mail", mail);
            startActivity(intent);
        }
        ...
    }
});
~~~
- GoogleMap을 실행하기 위해 필요한 permission들을 String 배열에 정의
~~~java
String[] REQUIRED_PERMISSIONS  = { Manifest.permission.ACCESS_FINE_LOCATION, Manifest.permission.ACCESS_COARSE_LOCATION };
~~~
- GoogleMap 객체를 파라미터로 제공할 수 있을 때(사용할 준비가 되었을 때) onMapReady() 메소드 호출
~~~java
SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager().findFragmentById(R.id.map);
mapFragment.getMapAsync(this);
...
@Override
public void onMapReady(final GoogleMap googleMap) {
    mMap = googleMap;
    setDefaultLocation();  //초기위치 서울로 이동

    // 위치 퍼미션을 가지고 있는지 확인
    int hasFineLocationPermission = ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION);
    int hasCoarseLocationPermission = ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_COARSE_LOCATION);

    if (hasFineLocationPermission == PackageManager.PERMISSION_GRANTED && hasCoarseLocationPermission == PackageManager.PERMISSION_GRANTED) {
        startLocationUpdates();
    } else {
        if (ActivityCompat.shouldShowRequestPermissionRationale(this, REQUIRED_PERMISSIONS[0])) {
            Snackbar.make(mLayout, "이 앱을 실행하려면 위치 접근 권한이 필요합니다.", Snackbar.LENGTH_INDEFINITE).setAction("확인", new View.OnClickListener() {
                @Override
                public void onClick(View view) {
                    ActivityCompat.requestPermissions( MainActivity.this, REQUIRED_PERMISSIONS, PERMISSIONS_REQUEST_CODE);
                }
            }).show();
        } else {
            ActivityCompat.requestPermissions( this, REQUIRED_PERMISSIONS, PERMISSIONS_REQUEST_CODE);
        }
    }
    mMap.getUiSettings().setMyLocationButtonEnabled(true);
    ...
}
~~~
- 4개의 지하철역 좌표 객체 생성 후 마커 추가
~~~java
LatLng Gwanghwamun = new LatLng(37.5707456,126.973708); //(위도, 경도)
LatLng Hongdae = new LatLng(37.557527,126.9222782);
LatLng Gileum = new LatLng(37.6086541,127.0136683);
LatLng DDP = new LatLng(37.5644,127.0055713);

MarkerOptions[] markerOptions = new MarkerOptions[4];
markerOptions[0] = new MarkerOptions()
        .position(Gwanghwamun)
        .title("광화문역");
markerOptions[1] = new MarkerOptions()
        .position(Hongdae)
        .title("홍대입구역");
markerOptions[2] = new MarkerOptions()
        .position(Gileum)
        .title("길음역");
markerOptions[3] = new MarkerOptions()
        .position(DDP)
        .title("동대문역사문화공원역");

for(int i=0; i<4; i++){
    mMap.addMarker(markerOptions[i]);
}
~~~
- 위치 정보 제공이 허용되어 있지 않은 경우 default 위치(국민대 부근, (37.6119, 126.9955)) 보여주는 setDefaultLocation() 메소드 호출
~~~java
public void setDefaultLocation() {
    LatLng DEFAULT_LOCATION = new LatLng(37.6119, 126.9955);
    String markerTitle = "위치정보 가져올 수 없음";
    String markerSnippet = "위치 퍼미션과 GPS 활성 요부 확인하세요";

    if (currentMarker != null) currentMarker.remove();

    MarkerOptions markerOptions = new MarkerOptions();
    markerOptions.position(DEFAULT_LOCATION);
    markerOptions.title(markerTitle);
    markerOptions.snippet(markerSnippet);
    markerOptions.draggable(true);
    markerOptions.icon(BitmapDescriptorFactory.defaultMarker(BitmapDescriptorFactory.HUE_RED));
    currentMarker = mMap.addMarker(markerOptions);
    
    CameraUpdate cameraUpdate = CameraUpdateFactory.newLatLngZoom(DEFAULT_LOCATION, 15);
    mMap.moveCamera(cameraUpdate);
}
~~~
- 마커 클릭하면 해당 지하철 역의 activity 실행
~~~java
private String mail;
private String station[] = {"길음역","광화문역","동역사역","홍대입구역"};
...
Intent intent = getIntent();
mail = intent.getStringExtra("mail");
...
@Override
public void onMapReady(final GoogleMap googleMap) {
    ...
    mMap.setOnMarkerClickListener(this);
}
...
@Override
public boolean onMarkerClick(Marker marker) {
    for (int i=0;i<station.length;i++) {
        if (marker.getTitle().equals(station[i])) {
            Intent intent = new Intent(MainActivity.this, SearchActivity.class);
            intent.putExtra("mail", mail);
            intent.putExtra("station", station[i]);
            startActivity(intent);
        }
    }
    return true;
}
~~~
- 툴바에서 '뒤로가기(←)'를 클릭하였을 때 이전 화면으로 돌아갈 때 intent값 전달 추가 코드 작성(SearchActivity.java, ChatActivity.java)
~~~java
tb.setNavigationOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v){
        Intent intent = new Intent(this, 이동하고 싶은 activity의 class);
        intent.putExtra("mail", 사용자의 메일);
        intent.putExtra("station", 선택한 역);
        startActivity(intent);
    }
});
~~~
- 채팅방의 대화가 추가되어 ListView가 갱신될 때 하단으로 자동 스크롤
~~~java
lv_chating.setTranscriptMode(ListView.TRANSCRIPT_MODE_ALWAYS_SCROLL);
~~~
