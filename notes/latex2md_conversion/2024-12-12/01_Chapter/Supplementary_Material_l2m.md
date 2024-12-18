\documentclass[12pt,twoside]{article}

{float}
[english]{babel}
[utf8]{inputenc}
{amsmath}
{graphicx}
{epsfig}
[table]{xcolor}
{multirow}
[colorinlistoftodos]{todonotes}
[hidelinks]{hyperref}
[a4paper,hmargin=2cm,vmargin=0.8cm,includeheadfoot]{geometry}
[font=footnotesize]{caption}
{natbib}

{abbrvnat}
{authoryear,open={(},close={)}} 



[right]{lineno} 

[1]

\raggedbottom 
\linespread{1.25} 

\title{Supplementary Material}
{}

\begin{document}

In the following, we provide additional information on various technical details and complementary analyses from our study, which were not included in the main text primarily due to space reasons. These pages cover the derivation of the JR model differential equations (Section S1), the equations of the transfer functions of the four models (Section S2), the derivation of the stability analysis of JR and LW (Section S3), the stability analysis with low noise of JR and LW (Section S4), the phase plane analysis of JR (Section S5), the 4D JR connectivity analyses (Section S6), the comparison of connectivity parameter spaces between JR and MDF (Section S7), the reduced 3D parameter space of MDF (Section S8), the full model equations with a description of their parameters and standard alpha values (Section S9), and finally the additional information on previous models that influenced the four models studied in this paper as well as other existing alpha theories (Section S10).
Note that complete code for the generating figures in the following and in the main text is openly available at \url{github.com/griffithslab/Bastiaens2024_AlphaModels}.



\subsection*{S.1 Derivation of the JR Model Equations}

The Jansen-Rit and related models are often discussed in terms of a convolution integral for the synaptic impulse response function, as well as the corresponding equivalent second-order differential equation, which is typically what is used in numerical simulations. The mathematical relationship between these is however rarely given in literature sources, and so we provide that here, with a full derivation of the JR differential equation from its impulse response, using the Laplace transform as it simplifies convolution operations by turning them into algebraic manipulations in the Laplace domain.

The synaptic impulse response is defined as an alpha function, which is described by the following equations:
```{math}
\label{my_first_eqn}
	h(t) =     
	\begin{cases}
      \alpha \beta t e^{-\beta t}, & t \geq 0\\
      0 & \text{otherwise}
    \end{cases}
```
with $\alpha$ as the maximum amplitude of the PSP and $\beta$ the rate constant parameter. The first step consists of finding the Laplace transform of $h(t)$, denoted as $H(s)$, which is defined as follows:
\begin{eqnarray}
    H(s) = \mathcal{L}\{h(t)\} &=& \int_{0}^{\infty} h(t)e^{-st} \,dt \\
    &=& \int_{0}^{\infty} \alpha \beta t e^{-\beta t}e^{-st} \,dt \\
    &=& \int_{0}^{\infty} \alpha \beta t e^{(-\beta-s) t} \,dt \\
    &=& \lim_{b\to\infty} \left[ \int_{0}^{b} \alpha \beta t e^{(-\beta-s) t} \,dt\right]\\
    &=& \lim_{b\to\infty} \left(\left[ \alpha \beta t \frac{1}{-\beta -s}e^{(-\beta-s) t} \right]_0^b - \int_{0}^{b} \frac{\alpha \beta}{-\beta-s}e^{(-\beta-s) t}\,dt\right)\\
    &=& \frac{\alpha \beta}{-\beta -s}\lim_{b\to\infty}\left(be^{(-\beta -s)b}- \int_{0}^{b} e^{(-\beta-s) t}\,dt\right)\\
    &=&\frac{\alpha \beta}{\beta + s}\lim_{b\to\infty} \int_{0}^{b}e^{(-\beta -s)t}\,dt\\
    &=&\frac{\alpha \beta}{\beta + s}\lim_{b\to\infty} \left[ \frac{1}{-\beta -s}e^{(-\beta-s) t} \right]_0^b\\
    &=&\frac{\alpha \beta}{(\beta + s)^{2}}\lim_{b\to\infty} \left[1 - e^{(-\beta -s)b} \right]\\
    &=& \frac{\alpha \beta}{(\beta + s)^{2}}
\end{eqnarray}

Now, with an expression for $H(s)$ in the Laplace domain, and given that $y(t)$ is equal to the convolution of $h(t)$ and $x(t)$, we can represent this relationship in the Laplace domain as:
\begin{eqnarray}
    Y(s) &=& X(s)H(s)\\
    Y(s) &=& X(s)\frac{\alpha \beta}{(\beta + s)^{2}}\\
    (\beta +s)^{2}Y(s) &=& X(s)\alpha \beta\\
    s^{2}Y(s) + \beta^{2}Y(s) + 2\beta s Y(s) &=& \alpha \beta X(s)\\
    s^{2}Y(s) &=& \alpha \beta X(s) - 2\beta s Y(s) - \beta^{2}Y(s)
\end{eqnarray}
Since $s^{2}Y(s)$ corresponds to the second derivative in the time domain, translating equation (40) back into the time domain, we obtain:
```{math}
\ddot{y}(t) = \alpha \beta x(t) - 2\beta \dot{y}(t) - \beta^{2}y(t)
```
This corresponds to the commonly used JR second-order differential equation, which can be rewritten in the form of two first-order ODE's:
\begin{eqnarray}
    \dot{y}(t) &=& z(t)\\
    \dot{z}(t) &=& \alpha \beta x(t) -2\beta z(t) - \beta^{2}y(t)
\end{eqnarray}
with $y(t)$ representing the average postsynaptic membrane potential (output of the PSP block). 



\subsection*{S.2 Transfer Function of the Models}
In addition to comparing the numerical simulation outputs, we also simulated the analytical (or linearized) power spectra of the models. These analytical models are used for stability analysis, offering clear insights into how a system responds to changes in inputs. Moreover, they provide explicit solutions, enhancing our understanding of the system's behavior. The transfer functions for both the JR and MDF models are derived from graph control analysis. The equations for the LW model are sourced from {cite:t}`hartoyo2019parameter`, while those for the RRW model are from {cite:t}`robinson2002dynamics`.

:::{figure} ../static/Images/Supp_transfer_v1.png
:label: fig:TF_supp
:align: center


:::



:label: fig:image
:align: center

Caption for the image
:::



:label: fig:image
:align: center

Caption for the image
:::




:label: fig:image
:align: center

Caption for the image
:::




:label: fig:image
:align: center

Caption for the image
:::





```




```



```

:::{figure} ../static/Images/Analytical_Power_Spectra.png
:label: fig:TF_all_supp
:align: center


:::


\subsection*{S.3 Derivation of Stability Analysis for JR and LW}
For JR, similar to {cite:t}`grimbert2006bifurcation`, the fixed points are determined by setting the derivatives to 0. With some manipulations, the equilibrium points in the ($C, y_1 - y_2$) plane with $y = y_1 - y_2$ are equal to:

```{math}
y = \frac{A}{a}p + \frac{A}{a}C_2S(\frac{A}{a}C_1S(y) - \frac{B}{b}C_4S(\frac{A}{a}C_3S(y))
```

The stability of the fixed points is then defined using the Jacobian matrix

```{math}
:enumerated: False
\hspace{-1cm}
\mathbf{Y}_{i,j} =
\begin{bmatrix}
  \frac{\partial y_0}{\partial y_0} & 
    \frac{\partial y_0}{\partial y_1} & 
    \frac{\partial y_0}{\partial y_2} &
    \frac{\partial y_0}{\partial y_3} &
    \frac{\partial y_0}{\partial y_4} &
    \frac{\partial y_0}{\partial y_5 } \\[1ex] 
  \frac{\partial y_1}{\partial y_0} & 
    \frac{\partial y_1}{\partial y_1} & 
    \frac{\partial y_1}{\partial y_2} &
    \frac{\partial y_1}{\partial y_3} &
    \frac{\partial y_1}{\partial y_4} &
    \frac{\partial y_1}{\partial y_5 } \\[1ex]
  \frac{\partial y_2}{\partial y_0} & 
    \frac{\partial y_2}{\partial y_1} & 
    \frac{\partial y_2}{\partial y_2} &
    \frac{\partial y_2}{\partial y_3} &
    \frac{\partial y_2}{\partial y_4} &
    \frac{\partial y_2}{\partial y_5 } \\[1ex]
  \frac{\partial y_3}{\partial y_0} & 
    \frac{\partial y_3}{\partial y_1} & 
    \frac{\partial y_3}{\partial y_2} &
    \frac{\partial y_3}{\partial y_3} &
    \frac{\partial y_3}{\partial y_4} &
    \frac{\partial y_3}{\partial y_5 } \\[1ex] 
  \frac{\partial y_4}{\partial y_0} & 
    \frac{\partial y_4}{\partial y_1} & 
    \frac{\partial y_4}{\partial y_2} &
    \frac{\partial y_4}{\partial y_3} &
    \frac{\partial y_4}{\partial y_4} &
    \frac{\partial y_4}{\partial y_5 } \\[1ex]
  \frac{\partial y_5}{\partial y_0} & 
    \frac{\partial y_5}{\partial y_1} & 
    \frac{\partial y_5}{\partial y_2} &
    \frac{\partial y_5}{\partial y_3} &
    \frac{\partial y_5}{\partial y_4} &
    \frac{\partial y_5}{\partial y_5 } 
\end{bmatrix}
= 
\begin{bmatrix}
  0 & 
    0 & 
    0 &
    1 &
    0 &
    0 \\[1ex] 
  0 & 
    0 & 
    0 &
    0 &
    1 &
    0 \\[1ex]
  0 & 
    0 & 
    0 &
    0 &
    0 &
    1 \\[1ex]
  -a^2 & 
    AaS'(y) & 
    -AaS'(y) &
    -2a &
    0 &
    0 \\[1ex]
  AaC_{2}C_{1}S'(C_{1}y_0(y)) & 
    -a^2 & 
    0 &
    0 &
    -2a &
    0 \\[1ex]
  BbC_{4}C_{3}S'(C_{3}y_0(y)) & 
    0 & 
    -b^2 &
    0 &
    0 &
    -2b
\end{bmatrix}
```
with $y$ corresponding to the fixed point of interest and $y_0(y) = \frac{A}{a}S(y)$. Stability is then defined by calculating the eigenvalues of the matrix $\mathbf{Y}$ for each fixed point, and looking at the sign of the real part of the eigenvalues. The system is stable if all the eigenvalues have a negative real part. If at least one of the eigenvalues has a positive real part, it is considered as an unstable fixed point. 

Using a similar method (estimation of the fixed point, following an assessment of the stability of the fixed points by looking at the real part of the eigenvalues of the Jacobian matrix), the LW equilibrium points' stability was also determined. The full calculation and equations are detailed in the appendix of {cite:t}`hartoyo2019parameter` and also in Supplementary S.6. Briefly: 

The equilibrium point equations can be reduced to:
\begin{eqnarray}
    0 &=& -V_e + V_{er} + \psi_{ee}(V_e)I_{ee} + \psi_ie(V_e)I_{ie} \\
    0 &=& -V_i + V_{ir} + \psi_{ei}(V_i)I_{ei} + \psi_{ii}(V_i)I_{ii}
\end{eqnarray}
with
\begin{eqnarray}
    I_{ee} &=& \frac{\Gamma_ee}{\gamma_e}N_{ee}^{\beta}S(V_e) + \frac{\Gamma_ee}{\gamma_e}p_{ee} \\
    I_{ei} &=& \frac{\Gamma_ee}{\gamma_e}N_{ei}^{\beta}S(V_e) + \frac{\Gamma_ee}{\gamma_e}p_{ei} \\
    I_{ie} &=& \frac{\Gamma_ie}{\gamma_i}N_{ie}^{\beta}S(V_i) + \frac{\Gamma_ie}{\gamma_i} \\
    I_{ii} &=& \frac{\Gamma_ie}{\gamma_i}N_{ii}^{\beta}S(V_i) + \frac{\Gamma_ie}{\gamma_i}
\end{eqnarray}

The fixed points for $V_e$ and $V_i$ are then estimated by finding the values for which values these two equations intersect.

The Jacobian matrix is: 

```{math}
:enumerated: False
\mathbf{F}_{i,j} =
\begin{bmatrix}
  \frac{\partial V_e}{\partial V_e} & 
    \frac{\partial V_e}{\partial V_i} & 
    \frac{\partial V_e}{\partial I_{ee}} &
    \frac{\partial V_e}{\partial I_{ei}} &
    \frac{\partial V_e}{\partial I_{ie}} &
    \frac{\partial V_e}{\partial I_{ii}} &
    \frac{\partial V_e}{\partial U_{ee}} &
    \frac{\partial V_e}{\partial U_{ei}} &
    \frac{\partial V_e}{\partial U_{ie}} &
    \frac{\partial V_e}{\partial U_{ii}} \\[1ex] 
  \frac{\partial V_i}{\partial V_e} & 
    \frac{\partial V_i}{\partial V_i} & 
    \frac{\partial V_i}{\partial I_{ee}} &
    \frac{\partial V_i}{\partial I_{ei}} &
    \frac{\partial V_i}{\partial I_{ie}} &
    \frac{\partial V_i}{\partial I_{ii}} &
    \frac{\partial V_i}{\partial U_{ee}} &
    \frac{\partial V_i}{\partial U_{ei}} &
    \frac{\partial V_i}{\partial U_{ie}} &
    \frac{\partial V_i}{\partial U_{ii}} \\[1ex]
  \frac{\partial I_{ee}}{\partial V_e} & 
    \frac{\partial I_{ee}}{\partial V_i} & 
    \frac{\partial I_{ee}}{\partial I_{ee}} &
    \frac{\partial I_{ee}}{\partial I_{ei}} &
    \frac{\partial I_{ee}}{\partial I_{ie}} &
    \frac{\partial I_{ee}}{\partial I_{ii}} &
    \frac{\partial I_{ee}}{\partial U_{ee}} &
    \frac{\partial I_{ee}}{\partial U_{ei}} &
    \frac{\partial I_{ee}}{\partial U_{ie}} &
    \frac{\partial I_{ee}}{\partial U_{ii}} \\[1ex]
  \frac{\partial I_{ei}}{\partial V_e} & 
    \frac{\partial I_{ei}}{\partial V_i} & 
    \frac{\partial I_{ei}}{\partial I_{ee}} &
    \frac{\partial I_{ei}}{\partial I_{ei}} &
    \frac{\partial I_{ei}}{\partial I_{ie}} &
    \frac{\partial I_{ei}}{\partial I_{ii}} &
    \frac{\partial I_{ei}}{\partial U_{ee}} &
    \frac{\partial I_{ei}}{\partial U_{ei}} &
    \frac{\partial I_{ei}}{\partial U_{ie}} &
    \frac{\partial I_{ei}}{\partial U_{ii}} \\[1ex]
  \frac{\partial I_{ie}}{\partial V_e} & 
    \frac{\partial I_{ie}}{\partial V_i} & 
    \frac{\partial I_{ie}}{\partial I_{ee}} &
    \frac{\partial I_{ie}}{\partial I_{ei}} &
    \frac{\partial I_{ie}}{\partial I_{ie}} &
    \frac{\partial I_{ie}}{\partial I_{ii}} &
    \frac{\partial I_{ie}}{\partial U_{ee}} &
    \frac{\partial I_{ie}}{\partial U_{ei}} &
    \frac{\partial I_{ie}}{\partial U_{ie}} &
    \frac{\partial I_{ie}}{\partial U_{ii}} \\[1ex]
  \frac{\partial I_{ii}}{\partial V_e} & 
    \frac{\partial I_{ii}}{\partial V_i} & 
    \frac{\partial I_{ii}}{\partial I_{ee}} &
    \frac{\partial I_{ii}}{\partial I_{ei}} &
    \frac{\partial I_{ii}}{\partial I_{ie}} &
    \frac{\partial I_{ii}}{\partial I_{ii}} &
    \frac{\partial I_{ii}}{\partial U_{ee}} &
    \frac{\partial I_{ii}}{\partial U_{ei}} &
    \frac{\partial I_{ii}}{\partial U_{ie}} &
    \frac{\partial I_{ii}}{\partial U_{ii}} \\[1ex]
  \frac{\partial U_{ee}}{\partial V_e} & 
    \frac{\partial U_{ee}}{\partial V_i} & 
    \frac{\partial U_{ee}}{\partial I_{ee}} &
    \frac{\partial U_{ee}}{\partial I_{ei}} &
    \frac{\partial U_{ee}}{\partial I_{ie}} &
    \frac{\partial U_{ee}}{\partial I_{ii}} &
    \frac{\partial U_{ee}}{\partial U_{ee}} &
    \frac{\partial U_{ee}}{\partial U_{ei}} &
    \frac{\partial U_{ee}}{\partial U_{ie}} &
    \frac{\partial U_{ee}}{\partial U_{ii}} \\[1ex]
  \frac{\partial U_{ei}}{\partial V_e} & 
    \frac{\partial U_{ei}}{\partial V_i} & 
    \frac{\partial U_{ei}}{\partial I_{ee}} &
    \frac{\partial U_{ei}}{\partial I_{ei}} &
    \frac{\partial U_{ei}}{\partial I_{ie}} &
    \frac{\partial U_{ei}}{\partial I_{ii}} &
    \frac{\partial U_{ei}}{\partial U_{ee}} &
    \frac{\partial U_{ei}}{\partial U_{ei}} &
    \frac{\partial U_{ei}}{\partial U_{ie}} &
    \frac{\partial U_{ei}}{\partial U_{ii}} \\[1ex]
  \frac{\partial U_{ie}}{\partial V_e} & 
    \frac{\partial U_{ie}}{\partial V_i} & 
    \frac{\partial U_{ie}}{\partial I_{ee}} &
    \frac{\partial U_{ie}}{\partial I_{ei}} &
    \frac{\partial U_{ie}}{\partial I_{ie}} &
    \frac{\partial U_{ie}}{\partial I_{ii}} &
    \frac{\partial U_{ie}}{\partial U_{ee}} &
    \frac{\partial U_{ie}}{\partial U_{ei}} &
    \frac{\partial U_{ie}}{\partial U_{ie}} &
    \frac{\partial U_{ie}}{\partial U_{ii}} \\[1ex]
  \frac{\partial U_{ii}}{\partial V_e} & 
    \frac{\partial U_{ii}}{\partial V_i} & 
    \frac{\partial U_{ii}}{\partial I_{ee}} &
    \frac{\partial U_{ii}}{\partial I_{ei}} &
    \frac{\partial U_{ii}}{\partial I_{ie}} &
    \frac{\partial U_{ii}}{\partial I_{ii}} &
    \frac{\partial U_{ii}}{\partial U_{ee}} &
    \frac{\partial U_{ii}}{\partial U_{ei}} &
    \frac{\partial U_{ii}}{\partial U_{ie}} &
    \frac{\partial U_{ii}}{\partial U_{ii}}
\end{bmatrix}
```


which evaluates to 
```{math}
:enumerated: False
\mathbf{F}_{i,j} =
\begin{bmatrix}
 G(V_e)  & 
    0 & 
    \frac{\psi_{ee}(V_e)}{\tau_e} &
    0 &
    \frac{\psi_{ie}(V_e)}{\tau_e} &
    0 &
    0 &
    0 &
    0 &
    0 \\[1ex] 
  G_(V_i) & 
    0 & 
    \frac{\psi_{ei}(V_i)}{\tau_i} &
    0 &
    \frac{\psi_{ii}(V_i)}{\tau_i} &
    0 &
    0 &
    0 &
    0 &
    0 \\[1ex]
  0 & 
    0 & 
    0 &
    0 &
    0 &
    0 &
    1 &
    0 &
    0 &
    0\\[1ex]
  0 & 
    0 & 
    0 &
    0 &
    0 &
    0 &
    0 &
    1 &
    0 &
    0\\[1ex]
  0 & 
    0 & 
    0 &
    0 &
    0 &
    0 &
    0 &
    0 &
    1 &
    0\\[1ex]
  0 & 
    0 & 
    0 &
    0 &
    0 &
    0 &
    0 &
    0 &
    0 &
    1\\[1ex]
  \Gamma_e\gamma_{e}eN_{ee}^{\beta}S'(V_e)& 
    0 & 
    -\gamma_{e}^2 &
    0 &
    0 &
    0 &
    -2\gamma_e &
    0 &
    0 &
    0\\[1ex]
  \Gamma_e\gamma_{e}eN_{ei}^{\beta}S'(V_e)& 
    0 & 
    0 &
    -\gamma_{e}^2 &
    0 &
    0 &
    0 &
    -2\gamma_e &
    0 &
    0\\[1ex]
  0 & 
    \Gamma_i\gamma_{i}eN_{ie}^{\beta}S'(V_i) & 
    0 &
    0 &
    -\gamma_{i}^2 &
    0 &
    0 &
    0 &
    -2\gamma_i &
    0\\[1ex]
  0 & 
    \Gamma_i\gamma_{i}eN_{ii}^{\beta}S'(V_i) & 
    0 &
    0 &
    0 &
    -\gamma_{i}^2 &
    0 &
    0 &
    0 &
    -2\gamma_i
\end{bmatrix}
```

with 

\begin{eqnarray}
    G(V_e) &=&  \frac{1}{\tau_e}(-1 - \frac{I_{ee}}{|V_e^eq - V_{er}|} - \frac{I_{ie}}{|V_i^eq - V_{ir}|}) \\
    G(V_i) &=& \frac{1}{\tau_i}(-1 - \frac{I_{ei}}{|V_e^eq - V_{ir}|} - \frac{I_{ii}}{|V_i^eq - V_{ir}|})
\end{eqnarray}

We then replace $V_e$ and $V_i$ with the equilibrium points computed previously, and the real parts of the eigenvalues of this Jacobian matrix are then examined to assess their stability. 


\subsection*{S.4 Stability Analysis Low Noise JR and LW of Connectivity E-I parameters}

In the main text, we presented the stability analysis of the E-I connectivity parameters with standard input. Our aim was to demonstrate the changes in this analysis when low noise input is introduced, highlighting the differences between the JR and LW models. Specifically, we showed that in the JR model, a Hopf bifurcation occurs at the alpha rhythm. In contrast, the alpha rhythm generated with LW model is noise-driven, as without noise, it behaves as a damped oscillator and reaches a fixed point instead of oscillating. 

:::{figure}
:label: fig:Fixed_points
:align: center

![](../static/Images/Stability_3.png)
![](../static/Images/Stability_noise_2.png)
![](../static/Images/Short_Low_Noise.png)


:::


\subsection*{S.5 Phase plane of JR in 3D}

For the stability analyses in Fig. 11, we have only presented the phase plane with the pyramidal and inhibitory population output voltages. Considering the trajectory of the third excitatory neural population activity alongside these can provide a better understanding of the full picture however, as can be seen in Fig. S4.


:::{figure} ../static/Images/Appendix_stab.png
:label: fig:Stability3D
:align: center


:::

As seen in our previous phase plane analysis, for specific connectivity parameters, the system either reaches a fixed point or enters a limit cycle defining the frequency of oscillation. The results closely resemble those in Fig. 11, implying that the dynamics primarily involve interactions between the pyramidal and inhibitory populations, with minimal contribution from the third population in this case.





\subsection*{S.6 Comparison of MDF and JR connectivity parameter spaces}

By setting the parameters to be the same between JR and MDF, we compare the connectivity parameter space of the two models (Fig. S9).


:::{figure}
:label: fig:LI_CS
:align: center

![](../static/Images/Comp_JR_MR_with_gamma_5.png)
![](../static/Images/Comp_JR_MR_without_gamma_5.png)
![](../static/Images/MDF_Appendix.png)


:::

In the top row of Fig. S6, we compare JR against MDF with the self-inhibitory connection. We observe a similar triangular boundary shape within which the system oscillates. However, MDF tends oscillate at higher frequency that exceed the alpha range (Fig. S6, MDF top row, colors are brighter than JR). When the self-inhibitory connection is removed in MDF (Fig. S6, MDF bottom row), the system now oscillates at the alpha frequency. It does not present lower frequencies, such as those in the JR model where we have slower oscillations. Thus, MDF seems to oscillate at higher frequencies than JR. Nonetheless, we observe that the two models share this similar triangular shape with non-oscillatory behavior when $C_3$ and $C_4$ are too low, suggesting similar global dynamics. The main conclusion drawn from this analysis is that the self-inhibitory connection introduced in MDF grants the model the ability to generate oscillations at a higher frequency than alpha, a more challenging capability compared to JR. 


\subsection*{S.7 4D JR connectivity analysis}

In the JR model, our focus was specifically on $C_{3}$ ($P \rightarrow I$) and $C_{4}$ ($I \rightarrow P$) as the E-I loop, but there is also the interaction between excitatory interneurons and pyramidal cells ($C_{1}$ ($P \rightarrow E$) and $C_{2}$ ($E \rightarrow P$)) to consider. Typically, the ratio between these values is varied. By simulating time series for different values of $C$ with the standard ratio values ($C_{1}=C$, $C_{2}=0.8*C$, $C_{3}=0.25*C$ and $C_{4}=0.25*C$), we can infer that increasing values of C lead to a decrease in the frequency of oscillation up to a certain point (Fig. S5), which concurs with results from {cite:t}`jansen1995electroencephalogram`. \\

:::{figure} ../static/Images/JR_Varying_C_time_series.png
:label: fig:JR_Ctime
:align: center


:::

Changes in the frequency of oscillation as a function of connectivity ratios are presented in the form of 4D heatmaps in a 2D space (Fig. S6). The general trend observed is that higher connectivity values result in slower oscillations, as expected. 



:::{figure} ../static/Images/JR_Connection_2png_new.png
:label: fig:JR_Cconnection
:align: center


:::

To observe the different trends that emerge, we focused on the case where $C$ equals 135 and investigated the different possible combinations of parameters on the outer and inner axes (Fig. S7).

:::{figure} ../static/Images/JR_All_Config_new.png
:label: fig:JR_C135
:align: center


:::

Clear patterns emerge in two different cases. When $C_{3}$ ($P \rightarrow I$) and $C_{4}$ ($I \rightarrow P$) are on the outer axes, a continuous change in the frequency of oscillation is observed. Similarly, when comparing $C_{1}$ ($P \rightarrow E$) against $C_{3}$ ($P \rightarrow I$), a concrete pattern is evident, with more pronounced changes in the frequency of oscillation when $C_{3}$ is altered. These results reinforce the idea that the main loop influencing the frequency of oscillation is the interaction between the pyramidal and inhibitory populations, raising the question of whether adding an additional excitatory population is truly necessary, even though it would be more biologically realistic. 


:::{figure} ../static/Images/JR_Zoom_C2C4_full_new.png
:label: fig:JR_Czoomed
:align: center


:::




:label: fig:JR_CZommed2
:align: center


:::








{1cm}






\subsection*{S.8 3D parameter space with MDF}

We simplified the 5-dimensional connection parameter space into a 3-dimensional representation for the MDF model, using its linearized version. Stability is assessed by looking at the system's poles within the transfer function of the system.
The aim was to establish a parallel with the 3D 'xyz' corticocortical/corticothalamic/intrathalamic lumped gains reduced parameter space discussed in a number of studies using the RRW model (although for reasons of space we have not focused on that aspect of RRW in the present paper {cite:alp}`robinson2002dynamics;Nonerobinson2005multiscale;Noneroberts2012corticothalamic;Nonebreakspear2006unifying;Noneabeysuriya2015physiologically`), and determine the effects of the loops on the dynamics of the MDF model.



:::{figure}
:label: fig:3D_Moran
:align: center

![](../static/Images/3dmoran1.png)
![](../static/Images/3dmoran2.png)


:::

The aim here is to easily visualize the regions of stability and dynamics as a function of the 'loops', rather than a single connectivity parameter. As expected, with the increase in the self-inhibitory connection (z-axis), the dominant frequency of oscillation gradually shifts from theta to alpha and then to the beta range.





\subsection*{S.9 Full Model Equations}

Partial and diagrammatic presentations of the differential equations for each of the four models are given in Figs. 4-7. In this final Supplementary section, we provide the complete differential equations for each model, as well as tables describing the model parameters and state variables. 


\subsubsection*{Jansen-Rit model equations}

The differential equations for the JR model are
\begin{eqnarray}
    \dot{y}_{0}(t) &=& y_{3}(t)\\
    \dot{y}_{3}(t) &=& AaS[y_{1}(t)-y_{2}(t)] - 2ay_{3}(t) - a^{2}y_{0}(t)\\
    \dot{y}_{1}(t) &=& y_{4}(t)\\
    \dot{y}_{4}(t) &=& Aa(p(t) + C_{2}S[C_{1}y_{0}(t)]) - 2ay_{4}(t) - a^{2}y_{1}(t)\\
    \dot{y}_{2}(t) &=& y_{5}(t)\\
    \dot{y}_{5}(t) &=& BbC_{4}S[C_{3}y_{0}] - 2by_{5}(t) - b^{2}y_{2}(t)
\end{eqnarray}


Here and in the rest of this paper we have maintained the same notation as in {cite:t}`jansen1995electroencephalogram` where $y_0$, $y_1$, and $y_2$ correspond to the outputs of the pyramidal, excitatory, and inhibitory PSP block, respectively. $p(t)$ represents the external input applied to the system, usually noise. $A$ and $B$ define the maximum amplitude of excitatory and inhibitory PSP, respectively. $a$ and $b$ represent the collective effect of the inverse of the time constant of the passive membrane and the entirety of the spatially dispersed delays within the dendritic network for the excitatory and inhibitory populations, respectively. $C_1$ to $C_4$ are the connectivity constants.

For the connectivity parameters, we wanted to mention that $C_{1}$ and $C_{3}$ slightly differ from $C_{2}$ and $C_{4}$ in the mathematical expression. The JR model assumes equal synaptic input from the pyramidal cell population to the other two populations, setting these constants to 1. In contrast, the synaptic coefficients at the excitatory and inhibitory dendrites are varied (corresponding to $C_{1}$ ($P \rightarrow E$) and $C_{3}$ ($P \rightarrow I$)). Conversely, for pyramidal cells, the synaptic coefficients at their dendrites remain fixed (1 and -1 for excitatory and inhibitory interneurons, respectively), and excitatory and inhibitory neurons synapse onto pyramidal cells differently (represented by $C_{2}$ ($E \rightarrow P$) and $C_{4}$ ($I \rightarrow P$). Therefore, $C_{1}$ and $C_{3}$ function as synaptic coefficients, while $C_{2}$ and $C_{4}$ serve as connectivity constants, as illustrated in the detailed schematic. Mathematically, this means that $C_{1}$ and $C_{3}$ are applied within the nonlinear function, while  $C_{2}$ and $C_{4}$ are applied outside. However, in practical terms, all these parameters are described as connectivity parameters and can be considered analogous and interrelated. Furthermore, all the values are scaled by a global connectivity parameter. 
See {cite:t}`cook2021neural` for a further explanation of this nuanced aspect of the JR model system.

\begin{table}[H]
\centering 
\begin{tabular}{|c|p{10cm}|p{4cm}| }
\hline
Symbol & \multicolumn{1}{|c|}{Description} & \multicolumn{1}{c|}{Value}  \\ 
 \hline
{$e_{0}$} & Firing rate at threshold & 2.5 s$^{(-1)}$ \\ 
 \hline
 $V_{0}$ & Firing threshold	& 6 mV \\ 
 \hline
 r	& Slope reflecting the variance of firing thresholds within the population &	0.56 mV$^{(-1)}$ \\
 \hline
 A &	Maximum amplitude of excitatory PSP (EPSP)&	3.25 mV \\
 \hline
 B & Maximum amplitude of inhibitory PSP (IPSP) &22 mV \\
 \hline
 a and b &	Lumped representation of the sum of the reciprocal of the time constant of passive membrane and all other spatially distributed delays in the dendritic network	& a = 100 s$^{(-1)}$  b = 50 $s^{(-1)}$\\
\hline
$C_{1}$ & Connectivity constant: Represents the number of synapses made by the feed forward neurons to the dendrites of the excitatory feedback loop &	$C=C_{1}$ 135\\
\hline
$C_{2}$ & Connectivity constant: Proportional to the number of synapses made by the excitatory feedback loop to the dendrites of the feedforward neurons & $C_{2}=0.8C$\\
\hline
$C_{3}$ & Connectivity constant: number of synapses made by the feedforward neurons to the dendrites of the inhibitory feedback loop & $C_{3}=0.25C$\\
\hline
$C_{4}$	& Connectivity constant: Proportional to the number of synapses made by the inhibitory feedback loop to the dendrites of the feedforward neurons & $C_{4}=0.25C$\\
\hline
P(t) & External pulse density consisting of activity originating from adjacent and more distant cortical columns and from subcortical structures (e.g. thalamus) & Uniform noise (or normal, constant)\\
\hline
\end{tabular}
\caption*{**Table 4.  _JR parameters with biological descriptions and corresponding values to generate alpha rhythm_**} 
\label{tab:Jansen-Rit}
\end{table}

\subsubsection*{Moran-David-Friston model equations}

The form of the differential equations for the MDF model are
\begin{eqnarray}
    \dot{\nu}_{1} &=& i_{1}\\
    \dot{i}_{1} &=& \kappa_{e}H_{e}(\gamma_{1}S(\nu_{6}-a) + u) - 2\kappa_{e}i_{1} - \kappa_{e}^{2}\nu_{1}\\
    \dot{\nu}_{2} &=& i_{2}\\
    \dot{i}_{2} &=& \kappa_{e}H_{e}\gamma_{2}S(\nu_{1}) - 2\kappa_{e}i_{2} - \kappa_{e}^{2}\nu_{2}\\
    \dot{\nu}_{3} &=& i_{3}\\
    \dot{i}_{3} &=& \kappa_{i}H_{i}\gamma_{4}S(\nu_{7}) - 2\kappa_{i}i_{3} - \kappa_{i}^{2}\nu_{3}
\end{eqnarray}
\begin{eqnarray}
    \dot{\nu}_{6} &=& i_{2} - i_{3}\\
    \dot{\nu}_{4} &=& i_{4}\\
    \dot{i}_{4} &=& \kappa_{e}H_{e}\gamma_{3}S(\nu_{6}) - 2\kappa_{e}i_{4} - \kappa_{e}^{2}\nu_{4}\\
    \dot{\nu}_{5} &=& i_{5}\\
    \dot{i}_{5} &=& \kappa_{i}H_{i}\gamma_{5}S(\nu_{7}) - 2\kappa_{i}i_{5} - \kappa_{i}^{2}\nu_{5} \\
    \dot{\nu}_{7} &=& i_{4} - i_{5}
    {-0.5cm}
\end{eqnarray}
The $v_i$ values represent the membrane potential of the subpopulations and $i_i$ denoting their current. Specifically, $v_1$ and $i_1$ describe the excitatory interneurons, $v_{2,3,6}$ and $i_{2,3}$ the pyramidal cells, and finally $v_{4,5,7}$ and $i_{4,5}$ the inhibitory interneurons. The $\gamma_i$ values are the connection strengths between the populations. $H_e$ and $\kappa_e$ are the maximum amplitude and the rate constant associated with EPSP, respectively. Similarly, $H_i$ and $\kappa_i$ represent the same parameters for the IPSP. 


\begin{table}[H]
\begin{tabular}{|c|p{12cm}|p{2.5cm}| }
\hline
Symbol & \multicolumn{1}{|c|}{Description} & \multicolumn{1}{c|}{Value}  \\ 
 \hline
$\rho_{1}$ & For shape of sigmoid: Can straighten more or less the slope & 2 \\ 
 \hline
$\rho_{2}$ & For position of sigmoid: Can shift the curve right or left & 1 \\ 
 \hline
$H_{e}$ & Maximum amplitude of excitatory PSP (EPSP) & 10 mV \\%4 mV \\
 \hline
$H_{i}$ & Maximum amplitude of inhibitory PSP (IPSP) & 22 mV \\%32 mV\\
 \hline
$\kappa_{e}$ and $\kappa_{i}$ & Lumped representation of the sum of the rate constants of passive membrane and other spatially distributed delays in the dendritic tree & $\kappa_{e}= 250$ s$^{(-1)}$  $\kappa_{i}= 62.5$ s$^{(-1)}$\\
 \hline
$\gamma_{1}$ & Coupling strength: Between pyramidal cells and macrocolumn u (in excitatory spiny cells in granular layer) & 128\\
\hline
$\gamma_{2}$ & Coupling strength: Between excitatory spiny cells in granular layer and pyramidal cells & 128\\
\hline
$\gamma_{3}$ & Coupling strength: Between pyramidal cells (excitatory) and inhibitory interneurons & 64\\
\hline
$\gamma_{4}$ & Coupling strength: Between inhibitory interneurons and pyramidal cells & 64\\
\hline
$\gamma_{5}$ & Coupling strength: Inhibitory-Inhibitory coupling (recurrent connection) & 1 \\%16\\
\hline
\end{tabular}
\caption*{**Table 5.  _MDF parameters with biological descriptions and corresponding values to generate alpha rhythm_**}
\label{tab:Moran}
\end{table}



\subsubsection*{Liley-Wright model equations}

For the LW model, the differential equations are
{-0.3cm}
\begin{eqnarray}
    \tau_{e}\dot{V}_{e}(t) &=& V_{e}^{rest} - V_{e}(t) + \psi_{ee}(V_{e}(t))I_{ee}(t) + \psi_{ie}(V_{e}(t))I_{ie}(t)\\
    \tau_{i}\dot{V}_{i}(t) &=& V_{i}^{rest} - V_{i}(t) + \psi_{ei}(V_{i}(t))I_{ei}(t) + \psi_{ii}(V_{i}(t))I_{ii}(t)\\
    \dot{I}_{ee} &=& U_{ee}\\
    \dot{U}_{ee} &=& -2\gamma_{e}U_{ee}(t) - \gamma_{e}^{2}I_{ee}(t) + \Gamma_{e}\gamma_{e}e(N_{ee}^{\beta}S(V_{e}(t)) + p_{ee}(t))\\
    \dot{I}_{ei} &=& U_{ei}\\
    \dot{U}_{ei} &=& -2\gamma_{e}U_{ei}(t) - \gamma_{e}^{2}I_{ei}(t) + \Gamma_{e}\gamma_{e}e(N_{ei}^{\beta}S(V_{e}(t)) + p_{ei}(t))\\
    \dot{I}_{ie} &=& U_{ie}\\
    \dot{U}_{ie} &=& -2\gamma_{i}U_{ie}(t) - \gamma_{i}^{2}I_{ie}(t) + \Gamma_{i}\gamma_{i}e(N_{ie}^{\beta}S(V_{i}(t)))\\
    \dot{I}_{ii} &=& U_{ii}\\
    \dot{U}_{ii} &=& -2\gamma_{i}U_{ii}(t) - \gamma_{i}^{2}I_{ii}(t) + \Gamma_{i}\gamma_{i}e(N_{ii}^{\beta}S(V_{i}(t)))
    {-0.4cm}
\end{eqnarray}
$N_{xx}$ are the inter- and intra-connectivities between the two populations. $p_{ei}$ and $p_{ee}$ are the external inputs. $I_{xx}$ are the postsynaptic potentials, and $V_{xx}$ are the soma membrane potentials. $\Gamma_{e,i}$ and $\gamma_{e,i}$ are the peak amplitude and rate constant PSPs for excitatory and inhibitory population, respectively. The model also includes passive membrane time constants represented by $\tau_{e,i}$, mean resting membrane potentials $V^{r}_{e,i}$, and mean equilibrium potentials $V^{eq}_{e,i}$.

\begin{table}[H]
\begin{tabular}{|c|p{12cm}|p{2.5cm}| }
\hline
Symbol & \multicolumn{1}{|c|}{Description} & \multicolumn{1}{c|}{Value}  \\ 
 \hline
$S_{(e,i)}^{max}$ & Excitatory/Inhibitory population mean maximal firing rates & 500, 500 s$^{(-1)}$ \\ 
 \hline
$\mu_{(e,i)}$ & Excitatory/Inhibitory population thresholds (spike threshold) & -50, -50 mV \\ 
 \hline
$\sigma_{(e,i)}$ & Standard deviation for spike-threshold in excitatory/inhibitory population & 5, 5 mV\\
 \hline
$\Gamma_{e}$ & Excitatory postsynaptic potential peak amplitude (at the site of synaptic activation) & 0.71 mV\\%0.4 mV\\
 \hline
$\Gamma_{i}$ & Inhibitory postsynaptic potential peak amplitude (at the siyte of synaptic activation)	& 0.71 mV \\%0.8 mV\\
 \hline
$\gamma_{(e,i)}$ & Excitatory/Inhibitory postsynaptic potential rate constant & 300, 65 s$^{(-1)}$\\
\hline
$\tau_{(e,i)}$ & Passive membrane decay time constant & 0.094, 0.042 s \\
\hline
$V_{(e,i)}^{r}$ & Mean resting membrane potential & -70, -70 mV\\
\hline
$V_{(e,i)}^{eq}$ & Mean equilibrium potential associated with excitation or inhibition & 45, -90 mV\\
\hline
$N_{(ee,ei)}^{\beta}$ & Total number of connections that a cell of type e, i receives from excitatory cells via intra-cortical fibres (Weight connections) & 3000, 3000\\
\hline
$N_{(ie,ii)}^{\beta}$ & Total number of connections that a cell of type e,i receives from inhibitory cells via intra-cortical connections (Weight connections) & 500, 500\\
\hline
$p_{(ee,ei)}$ & Excitatory extra-cortical input to excitatory, inhibitory cells & 3.46, 5.07s$^{(-1)}$\\
\hline
$p_{(ie,ii)}$ & Inhibitory extra-cortical input to excitatory, inhibitory cells &	0, 0  s$^{(-1)}$\\
\hline


\end{tabular}
\caption*{**Table 7.  _LW parameters with biological descriptions and values to generate alpha rhythm_**}
\label{tab:Liley}
\end{table}


\subsubsection*{Robinson-Rennie-Wright model equations}

Finally, the differential equations of the RRW are as follows
{-0.3cm}
\begin{eqnarray}
    \frac{dV_{e}}{dt} &=& \dot{V}_{e}\\
    \frac{d\dot{V}_{e}}{dt} &=& \alpha \beta[\nu_{ee}\phi_{e} + \nu_{ei}S(V_{e}) + \nu_{es}S(V_{s}(t-t_{0}/2)) - (\frac{1}{\alpha}+\frac{1}{\beta})\dot{V}_{e} - V_{e}]\\
    \frac{dV_{s}}{dt} &=& \dot{V}_{s}\\
    \frac{d\dot{V}_{s}}{dt} &=& \alpha \beta[\nu_{se}\phi_{e}(t-t_{0}/2) + \nu_{sr}S_{r}(V_{r}) + \nu_{sn}\phi_{n} - (\frac{1}{\alpha}+\frac{1}{\beta})\dot{V}_{s} - V_{s}]\\
    \frac{dV_{r}}{dt} &=& \dot{V}_{r}\\
    \frac{d\dot{V}_{r}}{dt} &=& \alpha \beta[\nu_{re}\phi_{e}(t-t_{0}/2) + \nu_{rs}S(V_{s}) - (\frac{1}{\alpha}+\frac{1}{\beta})\dot{V}_{e} - V_{r}]\\
    \frac{d\phi_{e}}{dt} &=& \dot{\phi}_{e}\\
    \frac{d\dot{\phi}_{e}}{dt} &=& \gamma_{e}^{2}[S(V_{e}) - \frac{2}{\gamma_{e}}\dot{\phi}_{e}-\phi_{e}]
\end{eqnarray}

with $V_e$, $V_r$, and $V_s$ representing the potential of the cortical population, the reticular nucleus, and the relay nuclei, respectively. $\nu_{xx}$ denote the connection strengths parameters. $\alpha$ and $\beta$ refer to the decay and rise time of the impulse response, representing the  dendritic rate. $t_0$ is the conduction delay between thalamic and cortical projections. Finally, $\gamma_e$ stands for the cortical damping rate, which is exclusively applied to the cortical population. This final differential equation for determining $\phi_e$ is related to the PDE damped wave equation, used to consider spatial variations [@robinson1997propagation]. However, in the case of spatial uniformity, the wave equation simplifies to an ODE [@zhao2015generalized].


\begin{table}[H]
\begin{tabular}{|c|p{12cm}|p{2.5cm}| }
\hline
Symbol & \multicolumn{1}{|c|}{Description} & \multicolumn{1}{c|}{Value}  \\ 
 \hline
$Q_{max}$ & Maximum attainable firing rate of individual neurons & 340 s$^{(-1)}$\\ 
 \hline
$\sigma'\pi \sqrt{3}$ & Standard deviation of the threshold distribution in the neural population & 3.8$*\pi \sqrt{3} \approx $ 5.9  mV\\ 
 \hline
$\theta$ & Mean firing threshold & 12.92 mV \\
 \hline
$\gamma_{e}$ & Cortical damping rate (Axonal velocity/Range) & 116 $s^{(-1)}$\\
 \hline
$1/\alpha$ & Decay time (of impulse response, dendritic rate) & 83.33 $s^{-1}$\\
 \hline
$1/\beta$ & Rise time (of impulse response, dendritic rate) & 769.23 $s^{-1}$\\
\hline
$t_{0}$ & Corticothalamic loop delay (Loop distance/Axonal velocity = conduction delay through thalamic nuclei and projections) & 80 ms\\
\hline
$v_{ee}$ & $N_{ee}s_{ee}$: Mean number of synapses X strength of the response to a unit signal & 3.03 mVs\\
\hline
$-v_{ei}$ & $-N_{ei}s_{ei}$ & 6.00 mVs\\
\hline
$v_{es}$ & $N_{es}s_{es}$ & 2.06 mVs\\
\hline
$v_{se}$ & $N_{se}s_{se}$ & 2.18 mVs\\
\hline
$-v_{sr}$ & $-N_{sr}s_{sr}$ & 0.83 mVs\\
\hline
$v_{re}$ & $N_{re}s_{re}$ & 0.33 mVs\\
\hline
$v_{rs}$ & $N_{rs}s_{rs}$ & 0.03 mVs\\
\hline
$v_{sn}$ & $N_{sn}s_{sn}$ & 0.98 mVs\\
\hline
\end{tabular}
\caption*{**Table 6.  _RRW parameters with biological descriptions and values to generate alpha rhythm_**}
\label{tab:Robinson}
\end{table}




\subsection*{S.10 Additional background literature}

For interested readers, we provide here some further background literature on early history of NPMs and other alpha theories:

{Tracing the roots of NPMs: early history}~\\
The notion of neural _masses_ was introduced in various forms during the 1950s and 1960s [@beurle1956properties;@griffith1963field], and consolidated in the 1970s primarily through the highly influential work of Freeman, Wilson \& Cowan, Amari, and Nunez. It was Freeman who originally used the term 'neural mass action model' [@freeman1972linear;@freeman1972waves;@freeman1975mass], articulating many of the neurobiological and mathematical fundamentals as they are understood today in a wide-reaching monograph on the subject [@freeman1975mass]. Here, Freeman also 
develops the theory of 'K-sets' which are based on a hierarchy of interacting sets of neural populations or masses, and used to model neural population dynamics with ordinary differential equations (ODEs) to simulate mesoscopic local field potentials [@deschle2021validity]. The levels are designated as K0, KI, KII, and KIII, with the K0 set corresponding to a model characterized by non-interactive collections of neurons with globally common inputs and outputs, KI to pairs of interacting K0 sets, and so on. Freeman's research on the olfactory bulb and prepyriform cortex of cats and rabbits [@freeman1979nonlinear;@freeman1975mass] provides valuable experimental data that has been used to define mathematical formulations and parameter settings in many NMMs, which is further discussed in section 3.2.4. Furthermore, Freeman's contributions on the use of the sigmoidal operator for mapping membrane potential to firing rate remains a critical component of many NMMs, the validity of which will be elaborated on in section 4.2. Even though Freeman coined the term neural masses and laid much of the groundwork, many of the core mathematical principles of NMMs were first proposed in the work of Wilson \& Cowan (WC; {cite:alp}'wilson1972excitatory'), which itself builds upon earlier work by {cite:t}`beurle1956properties`. WC's implementation introduced and solidified an approach to modelling neural dynamics and brain function. This approach consists of analyzing the collective properties of a large number of neurons using methods from statistical mechanics rooted in the mean-field framework [@destexhe2009wilson;@chow2020before]. By omitting potential spatial arrangement of synaptic connections, their model offers a minimalistic NMM representation that has been leveraged to develop several simple yet biophysically plausible models (eg {cite:alp}`Kilpatrick2013;Nonesanz2015mathematical`). As shown in Fig. S11, the canonical WC model consists of two neural masses with one excitatory and one inhibitory population [@wilson1972excitatory;@sanz2015mathematical]. Two nonlinear ODEs describe the dynamics of those two synaptically coupled populations in the neocortex [@nakagawa2014delays;@cowan2016wilson]. The WC system is thus a coarse-grained description of the overall activity and mesoscale neuronal network structure of a patch of (usually cortical) tissue, as is typical of NPMs. By varying the connectivity strength and the input strength to each population, it is possible to generate a diversity of dynamical behaviors that are characteristic of observed activity in the brain, such as multistability, oscillations, traveling waves, and spatial patterns [@Kilpatrick2013]. 

:::{figure} ../static/Images/Fig3__WC.png
:label: fig:WC_topography
:align: center


:::


A simplified version of the WC equations shown in Fig. 3 has been previously implemented by {cite:t}`abeysuriya2018biophysical` in a network of neural masses to generate alpha oscillations. These two populations are described as follows:

\begin{eqnarray}
    \tau_{e}\frac{dE(t)}{dt} &=& -E(t) + S(w_{ee}E(t) + w_{ie}I(t) + P + \epsilon(t)) \\
    \tau_{i}\frac{dI(t)}{dt} &=& -I(t) + S(w_{ei}E(t) + \epsilon(t))
\end{eqnarray}

where $E$ and $I$ represent the activity of the excitatory and inhibitory neural populations in the form of mean firing rates, $\tau_{e/i}$ are the excitatory/inhibitory time constants, $w_{ab}$ are the local connection strengths from population $a$ to population $b$, $P$ is a constant external input to the excitatory neural population, and $\epsilon$ is a noise signal added to the system. The studied NMMs share similar parameters, with some variations such as the use of membrane potential instead of firing rates as the state variable, and the concatenation of the external input and noise term into a single variable.

Concurrently to WC and Freeman, Lopes da Silva and colleagues developed a point-process model of EEG alpha rhythm generated with a corticothalamic loop [@lopes1974model]. Specifically, these authors proposed a negative feedback loop between excitatory thalamocortical relay cells and inhibitory thalamic reticular neurons as the basis for generating certain brain rhythms, in a manner similar to the interacting E and I populations in the WC model. By applying linear systems analysis to investigate the influence of physiological parameters on neural periodic patterns, they established a novel approach to studying oscillatory dynamics in theoretical neuroscience that relied on analytical power spectra.

The Lopes da Silva model had a substantial impact on subsequent corticothalamic models and linear analysis tools [@cona2014thalamo;@bhattacharya2011thalamo].

A few years later, {cite:t}'zetterberg1978performance` 
built an extension of the model by adding a second cortical excitatory population in order to separately account for pyramidal cells and excitatory interneurons. Their work was then reprised and further popularized by {cite:t}'jansen1995electroencephalogram'. In the JR model, each neural population is described in two steps: a transformation of the incoming average pulse density of action potentials into an average postsynaptic membrane potential, followed by a sigmoidal function to perform the inverse conversion. Over the years, several extended versions of JR have been proposed [@wendling2000relevance;@david2003neural;@zavaglia2006neural;@sotero2007realistically], - including Moran et al., where they focused on steady-state spectral responses with a linearized approximation of the model [@moran2007neural]. Contemporaneous with these early conceptualizations and formulations of NMMs in the 1970s was the introduction of NFMs by Amari, Wilson \& Cowan, Nunez, and others. The `brain wave equation' model of [@nunez1974brain] is particularly important here as it was the first to attempt to describe neural activity across the entire cerebral cortex with an evolution in both time and space. This work was a major influence for several macroscale NFM formulations in the 1990s [@jirsa1996field;@wright1996dynamics;@robinson1997propagation]. The latter of these which was then extended in 2001 to include the thalamus, and subsequently used to investigate a wide range of brain states including sleep [@robinson2005multiscale;@abeysuriya2014prediction], epileptic seizures [@zhao2015generalized;@breakspear2006unifying], evoked responses [@kerr2008physiology], functional connectivity [@robinson2014determination], and alpha rhythms [@robinson2002dynamics;@robinson2005multiscale].

For a more detailed timeline and review on the development of NPMs and whole brain modelling in general, we refer the reader to {cite:t}`griffiths2022whole` and {cite:t}`chow2020before`. The early mathematical models reviewed there and above laid the groundwork for most NPM formulations used in theoretical neuroscience today. In particular, they form the basis for the four most widely studied models of the EEG alpha rhythm - Jansen-Rit (JR), Moran-David-Friston (MDF), Liley-Wright (LW) and Robinson-Rennie-Wright (RRW). 


{Pacemaker vs. Local Network vs. Global Network Alpha theories}~\\
As indicated in the main text, the theories of alpha in the literature can be grouped under three categories: _pacemaker_, _local network_, and _global network_ theories. For reasons of space we discuss only the second of these in this article. The following provide some further notes and references for the interested reader on the other two. 
The pacemaker theory suggests that intrinsic alpha oscillations are generated either in the thalamus, driven by pulvinar or and/or the lateral geniculate nucleus [@saalmann2012pulvinar;@lHorincz2009temporal;@hughes2011thalamic] or in the cortex, originating from the pyramidal cells located in layer V [@da1991neural;@connors1997making;@bollimunta2008neuronal]. However, pacemaker theories in general suffer from several severe limitations (see {cite:alt}'nunez2006electric' for an extensive discussion of this). For instance, pacemaker cells such as putative thalamic nuclei, if they exist, would have to function in a relatively autonomous fashion, having a highly restricted input from other oscillatory brain regions - a notion that has been critically questioned on anatomical grounds [@lopes1998dynamics;@steriade2005cellular]. Additionally, there are certain global EEG phenomena that remain unexplained, including the relative frequencies of major rhythms and sleep-wave variations. The second category, `local network' theories,  propose that alpha rhythms are produced by interactions between excitatory and inhibitory neural populations with dendritic response functions and saturating nonlinearities [@valdes2010white]. Finally, 'global network' theories posit that alpha rhythms are generated by large-scale networks rather than local circuits within a localized brain region. By disregarding complex dendritic response functions and finite intracortical propagation, models with a primary emphasis on global dynamics rely heavily on the propagation delays between distant anatomical structures to shape their dynamics [@nunez1995neocortical;@nunez2006theoretical;@valdes2010white]. 




\bibliography{references}


\end{document}