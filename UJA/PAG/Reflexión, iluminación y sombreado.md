## Reflexión
Hay dos tipos de modelo de reflexión

### Locales
Cuentan la luz directa que nos llega desde una fuente

### Globales
Iluminación directa (luz rebotada de otros objetos) prácticamente todos son fuentes de iluminación


### Prueba para ver si sincroniza


### Modelos de Reflexión

```
ImGui::Combo ("##MovType",(int*)&_active,"None\0Zoom\0Crane\0Dolly\0Pan\0Tilt\0Orbit\0\0");

_changed = ImGui::SliderFloat ("##Zoom",&_zoom,5,175,"%.0f degrees");

case Movement::Crane:
	{
		Imgui::SetWindowSize(ImVec2(15*ImGui::GetFontSize(),6*ImGui::GetFontSize()));
		bool up=false
		bool down= false
		up=ImGui::Button("^ Up ^",ImVec2 (6*ImGui::GetFontSize(),2*ImGui::GetFontSize()));
		
	}_
```