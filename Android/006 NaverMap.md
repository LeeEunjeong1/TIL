# NaverMap
addOnCameraIdleListener : 카메라의 움직임이 끝난 경우에 대한 이벤트 리스너를 등록합니다.

setOnMapClickListener : 클릭 이벤트 리스너를 지정합니다. 사용자가 지도를 클릭하면 listener의 NaverMap.OnMapClickListener.onMapClick(PointF, LatLng)이 호출됩니다. 단, 오버레이나 심벌이 클릭 이벤트를 소비한 경우 지도까지 이벤트가 전달되지 않습니다.

locationOverlay : 사용자의 현재 위치를 나타내는 오버레이. 이 오버레이는 지도에 단 하나만 존재하며, 인스턴스를 직접 생성할 수 없고 NaverMap.getLocationOverlay()를 이용해서 가져올 수 있습니다.

http://localhost:63342/-9fefdm5e2v6cm5rvebrz5x5v1bwd0awjee28q/PicALoca/map-sdk-3.14.0-javadoc.jar/com/naver/maps/map/NaverMap.html