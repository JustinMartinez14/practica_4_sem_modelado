# practica_4_sem_modelado
este repositorio es para subir la tarea del maestro cain
% Ejercicio 1: Sistema de disco rodante
% Parámetros del sistema
m = 10;     % masa del disco (kg)
r = 0.05;   % radio del disco (m)
k = 100;    % constante del resorte (N/m)
I = 0.5*m*r^2;  % momento de inercia del disco

% Condiciones iniciales
theta0 = 0;     % ángulo inicial (rad)
theta_dot0 = 2; % velocidad angular inicial (rad/s)
x0 = [theta0; theta_dot0];

% Tiempo de simulación
tspan = [0 10];

% Resolver el sistema usando ODE45
[t, x] = ode45(@(t,x) disco_rodante(t,x,m,r,k,I), tspan, x0);

% Extraer resultados
theta = x(:,1);
theta_dot = x(:,2);

% Graficar resultados
figure(1);
subplot(2,1,1);
plot(t, theta);
xlabel('Tiempo (s)');
ylabel('Ángulo θ (rad)');
title('Posición angular del disco');
grid on;

subplot(2,1,2);
plot(t, theta_dot);
xlabel('Tiempo (s)');
ylabel('Velocidad angular θ̇ (rad/s)');
title('Velocidad angular del disco');
grid on;

% Diagrama de fase
figure(2);
plot(theta, theta_dot);
xlabel('θ (rad)');
ylabel('θ̇ (rad/s)');
title('Diagrama de fase');
grid on;

% Función que define el sistema de ecuaciones diferenciales
function dxdt = disco_rodante(t, x, m, r, k, I)
    theta = x(1);
    theta_dot = x(2);
    
    % Ecuación diferencial: (3/2)mr²θ̈ + kr²θ = 0
    % Reorganizando: θ̈ = -(2k)/(3m) * θ
    theta_ddot = -(2*k)/(3*m) * theta;
    
    dxdt = [theta_dot; theta_ddot];
end
