# Analisis-suelo-
import streamlit as st

# Configuración de la página para móviles
st.set_page_config(page_title="App de Análisis de Suelo", layout="centered")

st.title("🌱 Diagnóstico de Suelos")
st.write("Carga los parámetros del laboratorio para obtener una interpretación inmediata.")

# 1. Formulario de Entrada de Datos
with st.form("analisis_suelo"):
    st.subheader("Datos del Lote")
    mo = st.number_input("Materia Orgánica (%)", min_value=0.0, max_value=10.0, step=0.1)
    psi = st.number_input("Sodio Intercambiable (PSI %)", min_value=0.0, max_value=100.0, step=0.1)
    porosidad = st.number_input("Porosidad de Aireación (%)", min_value=0.0, max_value=100.0, step=0.5)
    fosforo = st.number_input("Fósforo (P - ppm)", min_value=0.0, max_value=100.0, step=1.0)
    
    boton_diagnostico = st.form_submit_button("Generar Diagnóstico")

# 2. Lógica de Interpretación y Semáforos
if boton_diagnostico:
    st.divider()
    st.subheader("Resultados e Interpretación")

    col1, col2 = st.columns(2)

    # --- MATERIA ORGÁNICA ---
    with col1:
        if mo < 2.0:
            st.error(f"MO: {mo}% (Bajo)")
        elif 2.0 <= mo <= 3.5:
            st.warning(f"MO: {mo}% (Medio)")
        else:
            st.success(f"MO: {mo}% (Óptimo)")

    # --- SODIO (PSI) ---
    with col2:
        if psi < 7:
            st.success(f"PSI: {psi}% (Normal)")
        elif 7 <= psi <= 15:
            st.warning(f"PSI: {psi}% (Sódico)")
        else:
            st.error(f"PSI: {psi}% (Muy Sódico)")

    # --- POROSIDAD ---
    with col1:
        if porosidad < 10:
            st.error(f"Porosidad: {porosidad}% (Riesgo de Compactación)")
        else:
            st.success(f"Porosidad: {porosidad}% (Adecuada)")

    # --- FÓSFORO ---
    with col2:
        if fosforo < 15:
            st.error(f"Fósforo: {fosforo} ppm (Deficiente)")
        else:
            st.success(f"Fósforo: {fosforo} ppm (Suficiente)")

    # 3. Sugerencia Agronómica Dinámica
    st.info("💡 **Recomendación Preliminar:**")
    if psi > 7:
        st.write("- Se recomienda evaluar la aplicación de enmiendas de calcio (yeso) para desplazar el sodio.")
    if mo < 2.5:
        st.write("- Considerar la intensificación de cultivos de cobertura para mejorar el aporte de carbono.")

         
