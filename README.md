# Seguimientoproyectos2nv import { useState, useEffect } from 'react';
import { Calendar, Users, FileText, Clock, AlertTriangle, CheckCircle, BarChart2, MessageSquare, Target, BookOpen, Settings, Plus, Edit, Trash2, Eye, Download, Share2, X, User, Briefcase, Grid, List, GanttChart, ClipboardList, CheckSquare, TrendingUp, PieChart, Layers, Activity } from 'lucide-react';
import { BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer, LineChart, Line, PieChart as RechartsPieChart, Pie, Cell } from 'recharts';

const App = () => {
  const [activeTab, setActiveTab] = useState('overview');
  const [selectedProject, setSelectedProject] = useState(null);
  const [showAddProject, setShowAddProject] = useState(false);
  const [editingProject, setEditingProject] = useState(null);
  const [editingSession, setEditingSession] = useState(null);
  const [showAddSession, setShowAddSession] = useState(false);
  const [assignmentsView, setAssignmentsView] = useState('grid');
  const [selectedMember, setSelectedMember] = useState(null);
  const [showAddTask, setShowAddTask] = useState(false);
  const [editingTask, setEditingTask] = useState(null);
  const [projects, setProjects] = useState([
    {
      id: 1,
      name: 'Proyecto Efecty',
      client: 'Efecty',
      status: 'En Progreso',
      progress: 65,
      plannedProgress: 70, // Nuevo campo para avance planificado
      stoppers: ['Revisión de documentos', 'Aprobación de presupuesto'],
      teamCapacity: '70%',
      deliveryDate: '2025-03-15',
      commitments: ['Entrega de prototipo', 'Pruebas de usuario'],
      weeklyReport: 'Avance en desarrollo frontend. Pruebas unitarias completadas.',
      challenges: ['Integración con API externa', 'Recursos limitados'],
      startDate: '2024-12-01',
      endDate: '2025-03-15',
      tasks: [
        { id: 1, name: 'Análisis de requisitos', start: '2024-12-01', end: '2024-12-15', progress: 100, plannedProgress: 100, status: 'Completado' },
        { id: 2, name: 'Diseño UX/UI', start: '2024-12-10', end: '2025-01-10', progress: 80, plannedProgress: 85, status: 'En Progreso' },
        { id: 3, name: 'Desarrollo frontend', start: '2025-01-05', end: '2025-02-15', progress: 60, plannedProgress: 65, status: 'En Progreso' },
        { id: 4, name: 'Desarrollo backend', start: '2025-01-10', end: '2025-02-20', progress: 40, plannedProgress: 50, status: 'En Progreso' },
        { id: 5, name: 'Pruebas y QA', start: '2025-02-15', end: '2025-03-05', progress: 0, plannedProgress: 10, status: 'Pendiente' },
        { id: 6, name: 'Entrega final', start: '2025-03-05', end: '2025-03-15', progress: 0, plannedProgress: 0, status: 'Pendiente' }
      ],
      color: 'from-blue-500 to-indigo-600'
    },
    {
      id: 2,
      name: 'Proyecto Aseguradora Solidaria',
      client: 'Aseguradora Solidaria',
      status: 'Planeación',
      progress: 20,
      plannedProgress: 25,
      stoppers: ['Definición de requisitos', 'Asignación de recursos'],
      teamCapacity: '45%',
      deliveryDate: '2025-04-30',
      commitments: ['Documentación técnica', 'Reunión con stakeholders'],
      weeklyReport: 'Recolección de requerimientos. Diagramas de flujo en proceso.',
      challenges: ['Alcance no definido', 'Coordinación entre equipos'],
      startDate: '2024-12-15',
      endDate: '2025-04-30',
      tasks: [
        { id: 1, name: 'Recopilación de requerimientos', start: '2024-12-15', end: '2025-01-15', progress: 30, plannedProgress: 35, status: 'En Progreso' },
        { id: 2, name: 'Diseño de arquitectura', start: '2025-01-10', end: '2025-02-10', progress: 0, plannedProgress: 15, status: 'Pendiente' },
        { id: 3, name: 'Desarrollo módulo 1', start: '2025-02-01', end: '2025-03-15', progress: 0, plannedProgress: 0, status: 'Pendiente' },
        { id: 4, name: 'Desarrollo módulo 2', start: '2025-02-15', end: '2025-03-30', progress: 0, plannedProgress: 0, status: 'Pendiente' },
        { id: 5, name: 'Integración y pruebas', start: '2025-03-20', end: '2025-04-20', progress: 0, plannedProgress: 0, status: 'Pendiente' },
        { id: 6, name: 'Entrega y capacitación', start: '2025-04-20', end: '2025-04-30', progress: 0, plannedProgress: 0, status: 'Pendiente' }
      ],
      color: 'from-green-500 to-emerald-600'
    },
    {
      id: 3,
      name: 'Proyecto Digital Transformation',
      client: 'TechCorp',
      status: 'En Progreso',
      progress: 45,
      plannedProgress: 50,
      stoppers: ['Aprobación de diseño', 'Recursos técnicos'],
      teamCapacity: '60%',
      deliveryDate: '2025-05-20',
      commitments: ['Migración de datos', 'Capacitación del equipo'],
      weeklyReport: 'Diseño finalizado. Inicio de desarrollo backend.',
      challenges: ['Compatibilidad con sistemas legacy', 'Timeline ajustado'],
      startDate: '2024-11-20',
      endDate: '2025-05-20',
      tasks: [
        { id: 1, name: 'Análisis de sistemas', start: '2024-11-20', end: '2024-12-10', progress: 100, plannedProgress: 100, status: 'Completado' },
        { id: 2, name: 'Diseño arquitectura', start: '2024-12-05', end: '2025-01-15', progress: 100, plannedProgress: 100, status: 'Completado' },
        { id: 3, name: 'Desarrollo módulo core', start: '2025-01-15', end: '2025-03-15', progress: 30, plannedProgress: 40, status: 'En Progreso' },
        { id: 4, name: 'Integración APIs', start: '2025-02-01', end: '2025-03-30', progress: 15, plannedProgress: 25, status: 'En Progreso' },
        { id: 5, name: 'Migración de datos', start: '2025-03-15', end: '2025-04-30', progress: 0, plannedProgress: 5, status: 'Pendiente' },
        { id: 6, name: 'Pruebas finales', start: '2025-04-20', end: '2025-05-15', progress: 0, plannedProgress: 0, status: 'Pendiente' }
      ],
      color: 'from-purple-500 to-pink-600'
    }
  ]);
  const [sessions, setSessions] = useState([
    {
      id: 1,
      type: 'Internas',
      frequency: 'Semanal',
      purpose: 'Revisión de avances y bloqueadores',
      nextDate: '2025-12-10',
      participants: 'Equipo técnico',
      duration: '1 hora'
    },
    {
      id: 2,
      type: 'Clientes',
      frequency: 'Quincenal',
      purpose: 'Actualización de estado del proyecto',
      nextDate: '2025-12-18',
      participants: 'Cliente + Gerente de proyecto',
      duration: '45 minutos'
    }
  ]);
  const [teamMembers, setTeamMembers] = useState([
    {
      id: 1,
      name: 'Carlos Rodríguez',
      role: 'Desarrollador Frontend',
      avatar: 'https://placehold.co/40x40/3b82f6/ffffff?text=CR',
      projects: [
        { projectId: 1, projectName: 'Proyecto Efecty', hours: 24, tasks: ['Desarrollo de interfaz', 'Pruebas unitarias'], status: 'En Progreso' }
      ],
      availability: '80%',
      skills: ['React', 'JavaScript', 'Tailwind CSS']
    },
    {
      id: 2,
      name: 'María González',
      role: 'Desarrollador Backend',
      avatar: 'https://placehold.co/40x40/ef4444/ffffff?text=MG',
      projects: [
        { projectId: 1, projectName: 'Proyecto Efecty', hours: 20, tasks: ['API REST', 'Integración con base de datos'], status: 'En Progreso' },
        { projectId: 2, projectName: 'Proyecto Aseguradora Solidaria', hours: 12, tasks: ['Análisis de requerimientos'], status: 'Planeación' }
      ],
      availability: '60%',
      skills: ['Node.js', 'Python', 'PostgreSQL']
    },
    {
      id: 3,
      name: 'Andrés Martínez',
      role: 'Diseñador UX/UI',
      avatar: 'https://placehold.co/40x40/10b981/ffffff?text=AM',
      projects: [
        { projectId: 2, projectName: 'Proyecto Aseguradora Solidaria', hours: 16, tasks: ['Diseño de wireframes', 'Prototipado'], status: 'Planeación' }
      ],
      availability: '90%',
      skills: ['Figma', 'Adobe XD', 'User Research']
    },
    {
      id: 4,
      name: 'Laura Pérez',
      role: 'Project Manager',
      avatar: 'https://placehold.co/40x40/f59e0b/ffffff?text=LP',
      projects: [
        { projectId: 1, projectName: 'Proyecto Efecty', hours: 8, tasks: ['Coordinación del equipo', 'Gestión de riesgos'], status: 'En Progreso' },
        { projectId: 2, projectName: 'Proyecto Aseguradora Solidaria', hours: 12, tasks: ['Gestión de stakeholders', 'Planificación'], status: 'Planeación' }
      ],
      availability: '70%',
      skills: ['Scrum', 'Kanban', 'JIRA']
    },
    {
      id: 5,
      name: 'Javier Torres',
      role: 'DevOps Engineer',
      avatar: 'https://placehold.co/40x40/8b5cf6/ffffff?text=JT',
      projects: [
        { projectId: 3, projectName: 'Proyecto Digital Transformation', hours: 18, tasks: ['Configuración CI/CD', 'Infraestructura cloud'], status: 'En Progreso' }
      ],
      availability: '75%',
      skills: ['Docker', 'Kubernetes', 'AWS']
    }
  ]);

  // Existing functions remain unchanged...
  const addProject = (newProject) => {
    const colors = [
      'from-blue-500 to-indigo-600',
      'from-green-500 to-emerald-600',
      'from-purple-500 to-pink-600',
      'from-red-500 to-orange-600',
      'from-teal-500 to-cyan-600',
      'from-amber-500 to-yellow-600'
    ];
    const randomColor = colors[Math.floor(Math.random() * colors.length)];
    setProjects([...projects, { ...newProject, id: projects.length + 1, color: randomColor }]);
    setShowAddProject(false);
  };
  const updateProject = (updatedProject) => {
    setProjects(projects.map(p => p.id === updatedProject.id ? updatedProject : p));
    setEditingProject(null);
  };
  const deleteProject = (id) => {
    const updatedProjects = projects.filter(p => p.id !== id);
    setProjects(updatedProjects);
    const updatedTeamMembers = teamMembers.map(member => ({
      ...member,
      projects: member.projects.filter(proj => proj.projectId !== id)
    }));
    setTeamMembers(updatedTeamMembers);
    setSelectedProject(null);
    setEditingProject(null);
  };
  const addSession = (newSession) => {
    setSessions([...sessions, { ...newSession, id: sessions.length + 1 }]);
    setShowAddSession(false);
  };
  const updateSession = (updatedSession) => {
    setSessions(sessions.map(s => s.id === updatedSession.id ? updatedSession : s));
    setEditingSession(null);
  };
  const deleteSession = (id) => {
    setSessions(sessions.filter(s => s.id !== id));
    setEditingSession(null);
  };
  const addTask = (projectId, newTask) => {
    setProjects(projects.map(project => 
      project.id === projectId 
        ? { ...project, tasks: [...project.tasks, { ...newTask, id: project.tasks.length + 1 }] }
        : project
    ));
    setShowAddTask(false);
  };
  const updateTask = (projectId, updatedTask) => {
    setProjects(projects.map(project => 
      project.id === projectId 
        ? { 
            ...project, 
            tasks: project.tasks.map(task => 
              task.id === updatedTask.id ? updatedTask : task
            )
          }
        : project
    ));
    setEditingTask(null);
  };
  const deleteTask = (projectId, taskId) => {
    setProjects(projects.map(project => 
      project.id === projectId 
        ? { 
            ...project, 
            tasks: project.tasks.filter(task => task.id !== taskId)
          }
        : project
    ));
  };
  const getStatusColor = (status) => {
    switch (status) {
      case 'En Progreso': return 'bg-yellow-100 text-yellow-800 border-yellow-200';
      case 'Planeación': return 'bg-blue-100 text-blue-800 border-blue-200';
      case 'Completado': return 'bg-green-100 text-green-800 border-green-200';
      case 'Retrasado': return 'bg-red-100 text-red-800 border-red-200';
      case 'Pendiente': return 'bg-gray-100 text-gray-800 border-gray-200';
      default: return 'bg-gray-100 text-gray-800 border-gray-200';
    }
  };
  const getProgressColor = (progress) => {
    if (progress >= 80) return 'bg-green-500';
    if (progress >= 50) return 'bg-yellow-500';
    return 'bg-red-500';
  };

  // New Analytics Functions
  const getProjectAnalyticsData = () => {
    return projects.map(project => ({
      name: project.name,
      actual: project.progress,
      planned: project.plannedProgress,
      variance: project.progress - project.plannedProgress,
      status: project.status
    }));
  };

  const getTaskAnalyticsData = () => {
    const allTasks = [];
    projects.forEach(project => {
      project.tasks.forEach(task => {
        allTasks.push({
          name: `${project.name} - ${task.name}`,
          actual: task.progress,
          planned: task.plannedProgress,
          variance: task.progress - task.plannedProgress,
          status: task.status
        });
      });
    });
    return allTasks;
  };

  const getStatusDistribution = () => {
    const statusCount = {
      'En Progreso': 0,
      'Planeación': 0,
      'Completado': 0,
      'Retrasado': 0,
      'Pendiente': 0
    };
    
    projects.forEach(project => {
      statusCount[project.status] = (statusCount[project.status] || 0) + 1;
    });
    
    return Object.entries(statusCount).map(([name, value]) => ({ name, value }));
  };

  const getTeamCapacityData = () => {
    return teamMembers.map(member => ({
      name: member.name,
      capacity: 100 - parseInt(member.availability),
      projects: member.projects.length
    }));
  };

  // Rest of the components remain mostly unchanged...
  // ... [same as original code for other components] ...

  // Enhanced Project Details Component with Task Management
  const ProjectDetails = ({ project, onClose }) => {
    const calculateProjectProgress = () => {
      if (project.tasks.length === 0) return 0;
      const totalProgress = project.tasks.reduce((sum, task) => sum + task.progress, 0);
      return Math.round(totalProgress / project.tasks.length);
    };
    const updateProjectProgress = () => {
      const newProgress = calculateProjectProgress();
      setProjects(projects.map(p => 
        p.id === project.id ? { ...p, progress: newProgress } : p
      ));
    };
    useEffect(() => {
      updateProjectProgress();
    }, [project.tasks]);
    const handleEditProject = () => {
      onClose();
      setEditingProject(project);
    };
    return (
      <div className="bg-white rounded-lg shadow-xl overflow-hidden">
        <div className={`px-6 py-4 border-b ${project.color.split(' ')[0].replace('from-', 'bg-')} ${project.color.split(' ')[1].replace('to-', 'bg-')} flex justify-between items-center`}>
          <h3 className="text-lg font-medium text-white">Detalles del Proyecto: {project.name}</h3>
          <button onClick={onClose} className="text-white hover:text-gray-200">
            <X className="h-6 w-6" />
          </button>
        </div>
        <div className="p-6">
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div>
              <h4 className="text-sm font-medium text-gray-900 mb-3">Información General</h4>
              <div className="space-y-2 text-sm">
                <div className="flex justify-between">
                  <span className="text-gray-500">Cliente:</span>
                  <span className="font-medium">{project.client}</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-500">Estado:</span>
                  <span className={`font-medium ${getStatusColor(project.status).split(' ')[0]}`}>
                    {project.status}
                  </span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-500">Avance Actual:</span>
                  <span className="font-medium">{calculateProjectProgress()}%</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-500">Avance Planificado:</span>
                  <span className="font-medium">{project.plannedProgress}%</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-500">Varianza:</span>
                  <span className={`font-medium ${project.progress - project.plannedProgress >= 0 ? 'text-green-600' : 'text-red-600'}`}>
                    {project.progress - project.plannedProgress}%
                  </span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-500">Capacidad del Equipo:</span>
                  <span className="font-medium">{project.teamCapacity}</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-500">Fecha de Inicio:</span>
                  <span className="font-medium">{project.startDate}</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-500">Fecha de Entrega:</span>
                  <span className="font-medium">{project.endDate}</span>
                </div>
              </div>
            </div>
            <div>
              <h4 className="text-sm font-medium text-gray-900 mb-3">Avance Visual</h4>
              <div className="space-y-3">
                <div>
                  <div className="flex justify-between mb-1">
                    <span className="text-xs text-gray-500">Planificado</span>
                    <span className="text-xs font-medium text-gray-700">{project.plannedProgress}%</span>
                  </div>
                  <div className="w-full bg-gray-200 rounded-full h-2">
                    <div 
                      className="h-2 rounded-full bg-blue-500" 
                      style={{ width: `${project.plannedProgress}%` }}
                    ></div>
                  </div>
                </div>
                <div>
                  <div className="flex justify-between mb-1">
                    <span className="text-xs text-gray-500">Actual</span>
                    <span className="text-xs font-medium text-gray-700">{calculateProjectProgress()}%</span>
                  </div>
                  <div className="w-full bg-gray-200 rounded-full h-2">
                    <div 
                      className={`h-2 rounded-full ${getProgressColor(calculateProjectProgress())}`} 
                      style={{ width: `${calculateProjectProgress()}%` }}
                    ></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          {/* Tasks Section */}
          <div className="mt-8">
            <div className="flex justify-between items-center mb-4">
              <h4 className="text-lg font-medium text-gray-900">Tareas del Proyecto</h4>
              <button 
                onClick={() => {
                  setShowAddTask(true);
                  setSelectedProject(project);
                }}
                className="inline-flex items-center px-3 py-1.5 border border-transparent rounded-lg text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 transition-all duration-200"
              >
                <Plus className="h-4 w-4 mr-1" />
                Nueva Tarea
              </button>
            </div>
            <div className="space-y-3">
              {project.tasks.map((task) => (
                <div key={task.id} className="border border-gray-200 rounded-lg p-4 bg-gradient-to-r from-white to-gray-50 hover:shadow-md transition-shadow duration-200">
                  <div className="flex justify-between items-start mb-2">
                    <h5 className="font-medium text-gray-900">{task.name}</h5>
                    <div className="flex space-x-2">
                      <button 
                        onClick={() => {
                          setEditingTask(task);
                          setSelectedProject(project);
                        }}
                        className="text-indigo-600 hover:text-indigo-900 p-1"
                      >
                        <Edit className="h-4 w-4" />
                      </button>
                      <button 
                        onClick={() => deleteTask(project.id, task.id)}
                        className="text-red-600 hover:text-red-900 p-1"
                      >
                        <Trash2 className="h-4 w-4" />
                      </button>
                    </div>
                  </div>
                  <div className="grid grid-cols-2 md:grid-cols-5 gap-4 text-sm">
                    <div>
                      <span className="text-gray-500">Inicio:</span>
                      <div className="font-medium">{task.start}</div>
                    </div>
                    <div>
                      <span className="text-gray-500">Fin:</span>
                      <div className="font-medium">{task.end}</div>
                    </div>
                    <div>
                      <span className="text-gray-500">Progreso Actual:</span>
                      <div className="font-medium">{task.progress}%</div>
                    </div>
                    <div>
                      <span className="text-gray-500">Progreso Planificado:</span>
                      <div className="font-medium">{task.plannedProgress}%</div>
                    </div>
                    <div>
                      <span className="text-gray-500">Estado:</span>
                      <span className={`inline-flex items-center px-2 py-1 rounded-full text-xs font-medium ${getStatusColor(task.status)}`}>
                        {task.status}
                      </span>
                    </div>
                  </div>
                  <div className="mt-3 space-y-2">
                    <div className="flex justify-between text-xs">
                      <span>Planificado</span>
                      <span>Actual</span>
                    </div>
                    <div className="w-full bg-gray-200 rounded-full h-2">
                      <div 
                        className="h-2 rounded-full bg-blue-500 bg-opacity-50" 
                        style={{ width: `${task.plannedProgress}%` }}
                      ></div>
                      <div 
                        className={`h-2 rounded-full ${getProgressColor(task.progress)} absolute top-0`} 
                        style={{ width: `${task.progress}%` }}
                      ></div>
                    </div>
                    <div className="text-xs text-gray-500">
                      Varianza: <span className={task.progress - task.plannedProgress >= 0 ? 'text-green-600' : 'text-red-600'}>
                        {task.progress - task.plannedProgress}%
                      </span>
                    </div>
                  </div>
                </div>
              ))}
              {project.tasks.length === 0 && (
                <div className="text-center py-8 text-gray-500">
                  <ClipboardList className="h-12 w-12 mx-auto mb-2 text-gray-400" />
                  <p>No hay tareas asignadas a este proyecto.</p>
                  <p className="mt-1">¡Agrega la primera tarea para comenzar el seguimiento!</p>
                </div>
              )}
            </div>
          </div>
          {/* Original project sections */}
          <div className="mt-8">
            <h4 className="text-sm font-medium text-gray-900 mb-3">Bloqueadores</h4>
            <ul className="list-disc list-inside space-y-1">
              {project.stoppers.map((stopper, index) => (
                <li key={index} className="text-sm">{stopper}</li>
              ))}
            </ul>
          </div>
          <div className="mt-6">
            <h4 className="text-sm font-medium text-gray-900 mb-3">Compromisos</h4>
            <ul className="list-disc list-inside space-y-1">
              {project.commitments.map((commitment, index) => (
                <li key={index} className="text-sm">{commitment}</li>
              ))}
            </ul>
          </div>
          <div className="mt-6">
            <h4 className="text-sm font-medium text-gray-900 mb-3">Informe Semanal</h4>
            <p className="text-sm">{project.weeklyReport}</p>
          </div>
          <div className="mt-6">
            <h4 className="text-sm font-medium text-gray-900 mb-3">Logros y Retos</h4>
            <ul className="list-disc list-inside space-y-1">
              {project.challenges.map((challenge, index) => (
                <li key={index} className="text-sm">{challenge}</li>
              ))}
            </ul>
          </div>
          <div className="mt-8 flex justify-end space-x-3">
            <button 
              onClick={handleEditProject}
              className="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              <Edit className="h-4 w-4 mr-1" />
              Editar Proyecto
            </button>
            <button 
              onClick={onClose}
              className="inline-flex justify-center px-3 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              Cerrar
            </button>
          </div>
        </div>
      </div>
    );
  };

  // New Analytics Dashboard Component
  const AnalyticsDashboard = () => {
    const projectData = getProjectAnalyticsData();
    const taskData = getTaskAnalyticsData();
    const statusData = getStatusDistribution();
    const teamCapacityData = getTeamCapacityData();
    
    const COLORS = ['#0088FE', '#00C49F', '#FFBB28', '#FF8042', '#8884d8'];
    
    // Calculate overall metrics
    const totalProjects = projects.length;
    const projectsOnTrack = projects.filter(p => p.progress >= p.plannedProgress).length;
    const projectsAtRisk = projects.filter(p => p.progress < p.plannedProgress - 10).length;
    const avgVariance = (projects.reduce((sum, p) => sum + (p.progress - p.plannedProgress), 0) / projects.length).toFixed(1);
    
    return (
      <div className="space-y-8">
        {/* Key Metrics */}
        <div className="grid grid-cols-1 md:grid-cols-4 gap-6">
          <div className="bg-gradient-to-r from-blue-500 to-indigo-600 rounded-xl shadow-lg p-6 text-white">
            <div className="flex items-center">
              <div className="flex-shrink-0">
                <Layers className="h-8 w-8 text-blue-100" />
              </div>
              <div className="ml-5 w-0 flex-1">
                <dl>
                  <dt className="text-sm font-medium text-blue-100 truncate">Proyectos Totales</dt>
                  <dd className="text-2xl font-bold">{totalProjects}</dd>
                </dl>
              </div>
            </div>
          </div>
          <div className="bg-gradient-to-r from-green-500 to-emerald-600 rounded-xl shadow-lg p-6 text-white">
            <div className="flex items-center">
              <div className="flex-shrink-0">
                <CheckCircle className="h-8 w-8 text-green-100" />
              </div>
              <div className="ml-5 w-0 flex-1">
                <dl>
                  <dt className="text-sm font-medium text-green-100 truncate">Proyectos en Tiempo</dt>
                  <dd className="text-2xl font-bold">{projectsOnTrack}</dd>
                </dl>
              </div>
            </div>
          </div>
          <div className="bg-gradient-to-r from-yellow-500 to-orange-600 rounded-xl shadow-lg p-6 text-white">
            <div className="flex items-center">
              <div className="flex-shrink-0">
                <AlertTriangle className="h-8 w-8 text-yellow-100" />
              </div>
              <div className="ml-5 w-0 flex-1">
                <dl>
                  <dt className="text-sm font-medium text-yellow-100 truncate">Proyectos en Riesgo</dt>
                  <dd className="text-2xl font-bold">{projectsAtRisk}</dd>
                </dl>
              </div>
            </div>
          </div>
          <div className="bg-gradient-to-r from-purple-500 to-pink-600 rounded-xl shadow-lg p-6 text-white">
            <div className="flex items-center">
              <div className="flex-shrink-0">
                <TrendingUp className="h-8 w-8 text-purple-100" />
              </div>
              <div className="ml-5 w-0 flex-1">
                <dl>
                  <dt className="text-sm font-medium text-purple-100 truncate">Varianza Promedio</dt>
                  <dd className={`text-2xl font-bold ${avgVariance >= 0 ? 'text-green-200' : 'text-red-200'}`}>
                    {avgVariance}%
                  </dd>
                </dl>
              </div>
            </div>
          </div>
        </div>
        
        {/* Charts Section */}
        <div className="grid grid-cols-1 lg:grid-cols-2 gap-8">
          {/* Project Progress Comparison */}
          <div className="bg-white shadow rounded-lg p-6">
            <h3 className="text-lg font-medium text-gray-900 mb-4">Comparación de Avance por Proyecto</h3>
            <div className="h-80">
              <ResponsiveContainer width="100%" height="100%">
                <BarChart
                  data={projectData}
                  margin={{ top: 20, right: 30, left: 20, bottom: 5 }}
                >
                  <CartesianGrid strokeDasharray="3 3" />
                  <XAxis dataKey="name" />
                  <YAxis domain={[0, 100]} />
                  <Tooltip 
                    formatter={(value) => [`${value}%`, 'Porcentaje']}
                    labelStyle={{ fontWeight: 'bold' }}
                  />
                  <Legend />
                  <Bar dataKey="planned" name="Planificado" fill="#4F46E5" />
                  <Bar dataKey="actual" name="Actual" fill="#10B981" />
                </BarChart>
              </ResponsiveContainer>
            </div>
          </div>
          
          {/* Task Variance Analysis */}
          <div className="bg-white shadow rounded-lg p-6">
            <h3 className="text-lg font-medium text-gray-900 mb-4">Análisis de Varianza por Tarea</h3>
            <div className="h-80">
              <ResponsiveContainer width="100%" height="100%">
                <BarChart
                  data={taskData.slice(0, 10)} // Limit to top 10 tasks
                  margin={{ top: 20, right: 30, left: 20, bottom: 5 }}
                >
                  <CartesianGrid strokeDasharray="3 3" />
                  <XAxis dataKey="name" height={60} tick={{ fontSize: 10 }} angle={-45} textAnchor="end" />
                  <YAxis />
                  <Tooltip 
                    formatter={(value) => [`${value}%`, 'Varianza']}
                    labelStyle={{ fontWeight: 'bold' }}
                  />
                  <Legend />
                  <Bar dataKey="variance" name="Varianza" fill="#EF4444" />
                </BarChart>
              </ResponsiveContainer>
            </div>
          </div>
        </div>
        
        {/* Additional Charts */}
        <div className="grid grid-cols-1 lg:grid-cols-3 gap-8">
          {/* Project Status Distribution */}
          <div className="bg-white shadow rounded-lg p-6">
            <h3 className="text-lg font-medium text-gray-900 mb-4">Distribución por Estado</h3>
            <div className="h-64">
              <ResponsiveContainer width="100%" height="100%">
                <RechartsPieChart>
                  <Pie
                    data={statusData}
                    cx="50%"
                    cy="50%"
                    labelLine={false}
                    outerRadius={80}
                    fill="#8884d8"
                    dataKey="value"
                    nameKey="name"
                    label={({ name, percent }) => `${name}: ${(percent * 100).toFixed(0)}%`}
                  >
                    {statusData.map((entry, index) => (
                      <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
                    ))}
                  </Pie>
                  <Tooltip formatter={(value) => [value, 'Proyectos']} />
                </RechartsPieChart>
              </ResponsiveContainer>
            </div>
          </div>
          
          {/* Team Capacity Utilization */}
          <div className="bg-white shadow rounded-lg p-6">
            <h3 className="text-lg font-medium text-gray-900 mb-4">Capacidad del Equipo</h3>
            <div className="h-64">
              <ResponsiveContainer width="100%" height="100%">
                <BarChart
                  data={teamCapacityData}
                  layout="vertical"
                  margin={{ top: 20, right: 30, left: 100, bottom: 20 }}
                >
                  <CartesianGrid strokeDasharray="3 3" />
                  <XAxis type="number" domain={[0, 100]} />
                  <YAxis 
                    dataKey="name" 
                    type="category" 
                    width={100}
                    tick={{ fontSize: 12 }}
                  />
                  <Tooltip 
                    formatter={(value) => [`${value}%`, 'Capacidad Utilizada']}
                    labelStyle={{ fontWeight: 'bold' }}
                  />
                  <Bar dataKey="capacity" name="Capacidad Utilizada" fill="#8B5CF6" />
                </BarChart>
              </ResponsiveContainer>
            </div>
          </div>
          
          {/* Progress Trend */}
          <div className="bg-white shadow rounded-lg p-6">
            <h3 className="text-lg font-medium text-gray-900 mb-4">Tendencia de Avance</h3>
            <div className="h-64">
              <ResponsiveContainer width="100%" height="100%">
                <LineChart
                  data={projects.map(p => ({
                    name: p.name,
                    planned: p.plannedProgress,
                    actual: p.progress
                  }))}
                  margin={{ top: 20, right: 30, left: 20, bottom: 5 }}
                >
                  <CartesianGrid strokeDasharray="3 3" />
                  <XAxis dataKey="name" />
                  <YAxis domain={[0, 100]} />
                  <Tooltip 
                    formatter={(value) => [`${value}%`, 'Porcentaje']}
                    labelStyle={{ fontWeight: 'bold' }}
                  />
                  <Legend />
                  <Line type="monotone" dataKey="planned" name="Planificado" stroke="#4F46E5" strokeWidth={2} />
                  <Line type="monotone" dataKey="actual" name="Actual" stroke="#10B981" strokeWidth={2} />
                </LineChart>
              </ResponsiveContainer>
            </div>
          </div>
        </div>
        
        {/* Detailed Analytics Table */}
        <div className="bg-white shadow rounded-lg overflow-hidden">
          <div className="px-6 py-4 border-b border-gray-200">
            <h3 className="text-lg font-medium text-gray-900">Análisis Detallado de Proyectos</h3>
            <p className="mt-1 text-sm text-gray-500">Comparación detallada entre avance planificado y real</p>
          </div>
          <div className="overflow-x-auto">
            <table className="min-w-full divide-y divide-gray-200">
              <thead className="bg-gray-50">
                <tr>
                  <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Proyecto</th>
                  <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Avance Planificado</th>
                  <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Avance Real</th>
                  <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Varianza</th>
                  <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Estado</th>
                  <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Acciones</th>
                </tr>
              </thead>
              <tbody className="bg-white divide-y divide-gray-200">
                {projectData.map((project, index) => (
                  <tr key={index} className="hover:bg-gray-50">
                    <td className="px-6 py-4 whitespace-nowrap">
                      <div className="text-sm font-medium text-gray-900">{project.name}</div>
                    </td>
                    <td className="px-6 py-4 whitespace-nowrap">
                      <div className="text-sm text-gray-900">{project.planned}%</div>
                    </td>
                    <td className="px-6 py-4 whitespace-nowrap">
                      <div className="text-sm text-gray-900">{project.actual}%</div>
                    </td>
                    <td className="px-6 py-4 whitespace-nowrap">
                      <span className={`px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${
                        project.variance >= 0 
                          ? 'bg-green-100 text-green-800' 
                          : 'bg-red-100 text-red-800'
                      }`}>
                        {project.variance >= 0 ? '+' : ''}{project.variance}%
                      </span>
                    </td>
                    <td className="px-6 py-4 whitespace-nowrap">
                      <span className={`px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${
                        getStatusColor(project.status).split(' ')[0]
                      }`}>
                        {project.status}
                      </span>
                    </td>
                    <td className="px-6 py-4 whitespace-nowrap text-sm font-medium">
                      <button 
                        onClick={() => setSelectedProject(projects.find(p => p.name === project.name))}
                        className="text-indigo-600 hover:text-indigo-900"
                      >
                        Ver Detalles
                      </button>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </div>
        </div>
        
        {/* Recommendations Section */}
        <div className="bg-white shadow rounded-lg p-6">
          <h3 className="text-lg font-medium text-gray-900 mb-4">Recomendaciones</h3>
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div>
              <h4 className="text-sm font-medium text-gray-900 mb-2">Acciones Prioritarias</h4>
              <ul className="list-disc list-inside space-y-1 text-sm text-gray-600">
                <li>Revisar proyectos con varianza negativa mayor al 10%</li>
                <li>Ajustar fechas de entrega para tareas con bajo progreso</li>
                <li>Asignar más recursos a proyectos en riesgo</li>
                <li>Documentar causas de desviaciones significativas</li>
              </ul>
            </div>
            <div>
              <h4 className="text-sm font-medium text-gray-900 mb-2">Métricas Clave para Seguimiento</h4>
              <ul className="list-disc list-inside space-y-1 text-sm text-gray-600">
                <li>Varianza de avance (Actual vs Planificado)</li>
                <li>Porcentaje de tareas completadas a tiempo</li>
                <li>Capacidad disponible del equipo</li>
                <li>Número de bloqueadores activos</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    );
  };

  // Other components (ColorfulProjectCard, TaskForm, ProjectForm, SessionForm, SessionDetails, AssignmentDetails, GanttChartView, ColorfulAssignmentCard, MemberForm) remain unchanged
  // ... [same as original implementation] ...

  // ColorfulProjectCard Component
  const ColorfulProjectCard = ({ project, onView, onEdit, onDelete }) => {
    return (
      <div className={`bg-white rounded-xl shadow-lg overflow-hidden hover:shadow-xl transition-all duration-300 border-2 border-transparent hover:border-${project.color.split('-')[1] || 'blue'}-300`}>
        <div className={`h-2 bg-gradient-to-r ${project.color}`}></div>
        <div className="p-6">
          <div className="flex items-start justify-between">
            <div>
              <h3 className="text-xl font-bold text-gray-900 mb-1">{project.name}</h3>
              <p className="text-sm text-gray-600 mb-3">Cliente: {project.client}</p>
              <div className="flex flex-wrap gap-2 mb-4">
                <span className={`inline-flex items-center px-3 py-1 rounded-full text-xs font-medium bg-gradient-to-r ${project.color} text-white`}>
                  {project.status}
                </span>
                <span className="inline-flex items-center px-3 py-1 rounded-full text-xs font-medium bg-gray-100 text-gray-800">
                  {project.progress}% completado
                </span>
              </div>
              <div className="space-y-2 text-sm">
                <div className="flex items-center text-gray-600">
                  <Calendar className="h-4 w-4 mr-2 text-gray-500" />
                  <span>{project.startDate} - {project.endDate}</span>
                </div>
                <div className="flex items-center text-gray-600">
                  <Users className="h-4 w-4 mr-2 text-gray-500" />
                  <span>Capacidad: {project.teamCapacity}</span>
                </div>
              </div>
            </div>
            <div className="flex flex-col space-y-2">
              <div className="w-16 h-16 rounded-full bg-gradient-to-r from-gray-100 to-gray-200 flex items-center justify-center">
                <FileText className={`h-8 w-8 text-${project.color.split('-')[1] || 'blue'}-600`} />
              </div>
            </div>
          </div>
          <div className="mt-4">
            <div className="w-full bg-gray-200 rounded-full h-3">
              <div 
                className={`h-3 rounded-full bg-gradient-to-r ${project.color}`} 
                style={{ width: `${project.progress}%` }}
              ></div>
            </div>
          </div>
          <div className="mt-6 flex justify-end space-x-3">
            <button 
              onClick={() => onView(project)}
              className="inline-flex items-center px-3 py-1.5 border border-gray-300 rounded-lg text-sm font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 transition-colors duration-200"
            >
              <Eye className="h-4 w-4 mr-1" />
              Ver
            </button>
            <button 
              onClick={() => onEdit(project)}
              className="inline-flex items-center px-3 py-1.5 border border-transparent rounded-lg text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 transition-all duration-200"
            >
              <Edit className="h-4 w-4 mr-1" />
              Editar
            </button>
            <button 
              onClick={() => onDelete(project.id)}
              className="inline-flex items-center px-3 py-1.5 border border-transparent rounded-lg text-sm font-medium text-white bg-gradient-to-r from-red-600 to-orange-600 hover:from-red-700 hover:to-orange-700 focus:outline-none focus:ring-2 focus:ring-offset-2 transition-all duration-200"
            >
              <Trash2 className="h-4 w-4 mr-1" />
              Eliminar
            </button>
          </div>
        </div>
      </div>
    );
  };

  // Task Form Component
  const TaskForm = ({ task, onSave, onCancel, projectId }) => {
    const initialFormData = {
      name: task?.name || '',
      start: task?.start || '',
      end: task?.end || '',
      progress: task?.progress?.toString() || '0',
      plannedProgress: task?.plannedProgress?.toString() || '0',
      status: task?.status || 'Pendiente'
    };
    const [formData, setFormData] = useState(initialFormData);
    useEffect(() => {
      if (task) {
        setFormData({
          name: task.name || '',
          start: task.start || '',
          end: task.end || '',
          progress: task.progress?.toString() || '0',
          plannedProgress: task.plannedProgress?.toString() || '0',
          status: task.status || 'Pendiente'
        });
      }
    }, [task]);
    const handleChange = (e) => {
      setFormData({
        ...formData,
        [e.target.name]: e.target.value
      });
    };
    const handleSubmit = (e) => {
      e.preventDefault();
      const updatedTask = {
        id: task?.id || null,
        name: formData.name,
        start: formData.start,
        end: formData.end,
        progress: parseInt(formData.progress) || 0,
        plannedProgress: parseInt(formData.plannedProgress) || 0,
        status: formData.status
      };
      onSave(projectId, updatedTask);
    };
    return (
      <div className="bg-white rounded-lg shadow-xl overflow-hidden">
        <div className="px-6 py-4 border-b border-gray-200 flex justify-between items-center">
          <h3 className="text-lg font-medium text-gray-900">
            {task ? 'Editar Tarea' : 'Nueva Tarea'}
          </h3>
          <button onClick={onCancel} className="text-gray-400 hover:text-gray-500">
            <X className="h-6 w-6" />
          </button>
        </div>
        <form onSubmit={handleSubmit} className="p-6">
          <div className="space-y-4">
            <div>
              <label className="block text-sm font-medium text-gray-700">Nombre de la Tarea</label>
              <input 
                type="text" 
                name="name" 
                value={formData.name}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Fecha de Inicio</label>
              <input 
                type="date" 
                name="start" 
                value={formData.start}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Fecha de Fin</label>
              <input 
                type="date" 
                name="end" 
                value={formData.end}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Progreso Actual (%)</label>
              <input 
                type="number" 
                name="progress" 
                value={formData.progress}
                onChange={handleChange}
                min="0" 
                max="100" 
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Progreso Planificado (%)</label>
              <input 
                type="number" 
                name="plannedProgress" 
                value={formData.plannedProgress}
                onChange={handleChange}
                min="0" 
                max="100" 
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Estado</label>
              <select 
                name="status" 
                value={formData.status}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              >
                <option value="Pendiente">Pendiente</option>
                <option value="En Progreso">En Progreso</option>
                <option value="Completado">Completado</option>
                <option value="Retrasado">Retrasado</option>
              </select>
            </div>
          </div>
          <div className="mt-6 flex justify-end space-x-3">
            <button 
              type="button" 
              onClick={onCancel}
              className="inline-flex justify-center px-4 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              Cancelar
            </button>
            <button 
              type="submit" 
              className="inline-flex justify-center px-4 py-2 text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 border border-transparent rounded-md hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              {task ? 'Actualizar' : 'Guardar'}
            </button>
          </div>
        </form>
      </div>
    );
  };

  // Project Form Component
  const ProjectForm = ({ project, onSave, onCancel }) => {
    const initialFormData = {
      name: project?.name || '',
      client: project?.client || '',
      status: project?.status || 'Planeación',
      progress: project?.progress?.toString() || '0',
      plannedProgress: project?.plannedProgress?.toString() || '0',
      stoppers: project?.stoppers?.join(', ') || '',
      teamCapacity: project?.teamCapacity || '',
      deliveryDate: project?.deliveryDate || '',
      commitments: project?.commitments?.join(', ') || '',
      weeklyReport: project?.weeklyReport || '',
      challenges: project?.challenges?.join(', ') || '',
      startDate: project?.startDate || '',
      endDate: project?.endDate || ''
    };
    const [formData, setFormData] = useState(initialFormData);
    useEffect(() => {
      if (project) {
        setFormData({
          name: project.name || '',
          client: project.client || '',
          status: project.status || 'Planeación',
          progress: project.progress?.toString() || '0',
          plannedProgress: project.plannedProgress?.toString() || '0',
          stoppers: project.stoppers?.join(', ') || '',
          teamCapacity: project.teamCapacity || '',
          deliveryDate: project.deliveryDate || '',
          commitments: project.commitments?.join(', ') || '',
          weeklyReport: project.weeklyReport || '',
          challenges: project.challenges?.join(', ') || '',
          startDate: project.startDate || '',
          endDate: project.endDate || ''
        });
      }
    }, [project]);
    const handleChange = (e) => {
      setFormData({
        ...formData,
        [e.target.name]: e.target.value
      });
    };
    const handleSubmit = (e) => {
      e.preventDefault();
      const updatedProject = {
        id: project?.id || null,
        name: formData.name,
        client: formData.client,
        status: formData.status,
        progress: parseInt(formData.progress) || 0,
        plannedProgress: parseInt(formData.plannedProgress) || 0,
        stoppers: formData.stoppers.split(',').map(s => s.trim()).filter(s => s),
        teamCapacity: formData.teamCapacity,
        deliveryDate: formData.deliveryDate,
        commitments: formData.commitments.split(',').map(c => c.trim()).filter(c => c),
        weeklyReport: formData.weeklyReport,
        challenges: formData.challenges.split(',').map(c => c.trim()).filter(c => c),
        startDate: formData.startDate,
        endDate: formData.endDate
      };
      onSave(updatedProject);
    };
    return (
      <div className="bg-white rounded-lg shadow-xl overflow-hidden">
        <div className="px-6 py-4 border-b border-gray-200 flex justify-between items-center">
          <h3 className="text-lg font-medium text-gray-900">
            {project ? 'Editar Proyecto' : 'Nuevo Proyecto'}
          </h3>
          <button onClick={onCancel} className="text-gray-400 hover:text-gray-500">
            <X className="h-6 w-6" />
          </button>
        </div>
        <form onSubmit={handleSubmit} className="p-6">
          <div className="space-y-4">
            <div>
              <label className="block text-sm font-medium text-gray-700">Nombre del Proyecto</label>
              <input 
                type="text" 
                name="name" 
                value={formData.name}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Cliente</label>
              <input 
                type="text" 
                name="client" 
                value={formData.client}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Estado</label>
              <select 
                name="status" 
                value={formData.status}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              >
                <option value="Planeación">Planeación</option>
                <option value="En Progreso">En Progreso</option>
                <option value="Completado">Completado</option>
                <option value="Retrasado">Retrasado</option>
              </select>
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Avance Actual (%)</label>
              <input 
                type="number" 
                name="progress" 
                value={formData.progress}
                onChange={handleChange}
                min="0" 
                max="100" 
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Avance Planificado (%)</label>
              <input 
                type="number" 
                name="plannedProgress" 
                value={formData.plannedProgress}
                onChange={handleChange}
                min="0" 
                max="100" 
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Bloqueadores (separados por coma)</label>
              <textarea 
                name="stoppers" 
                value={formData.stoppers}
                onChange={handleChange}
                rows="2" 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              ></textarea>
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Capacidad del Equipo</label>
              <input 
                type="text" 
                name="teamCapacity" 
                value={formData.teamCapacity}
                onChange={handleChange}
                placeholder="Ej: 70%" 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Fecha de Inicio</label>
              <input 
                type="date" 
                name="startDate" 
                value={formData.startDate}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Fecha de Entrega</label>
              <input 
                type="date" 
                name="endDate" 
                value={formData.endDate}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Compromisos (separados por coma)</label>
              <textarea 
                name="commitments" 
                value={formData.commitments}
                onChange={handleChange}
                rows="2" 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              ></textarea>
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Informe Semanal</label>
              <textarea 
                name="weeklyReport" 
                value={formData.weeklyReport}
                onChange={handleChange}
                rows="3" 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              ></textarea>
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Logros/Reto (separados por coma)</label>
              <textarea 
                name="challenges" 
                value={formData.challenges}
                onChange={handleChange}
                rows="2" 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              ></textarea>
            </div>
          </div>
          <div className="mt-6 flex justify-end space-x-3">
            <button 
              type="button" 
              onClick={onCancel}
              className="inline-flex justify-center px-4 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              Cancelar
            </button>
            <button 
              type="submit" 
              className="inline-flex justify-center px-4 py-2 text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 border border-transparent rounded-md hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              {project ? 'Actualizar' : 'Guardar'}
            </button>
          </div>
        </form>
      </div>
    );
  };

  // Session Form Component
  const SessionForm = ({ session, onSave, onCancel }) => {
    const initialFormData = {
      type: session?.type || 'Internas',
      frequency: session?.frequency || 'Semanal',
      purpose: session?.purpose || '',
      nextDate: session?.nextDate || '',
      participants: session?.participants || '',
      duration: session?.duration || ''
    };
    const [formData, setFormData] = useState(initialFormData);
    useEffect(() => {
      if (session) {
        setFormData({
          type: session.type || 'Internas',
          frequency: session.frequency || 'Semanal',
          purpose: session.purpose || '',
          nextDate: session.nextDate || '',
          participants: session.participants || '',
          duration: session.duration || ''
        });
      }
    }, [session]);
    const handleChange = (e) => {
      setFormData({
        ...formData,
        [e.target.name]: e.target.value
      });
    };
    const handleSubmit = (e) => {
      e.preventDefault();
      const saveSession = {
        id: session?.id || sessions.length + 1,
        type: formData.type,
        frequency: formData.frequency,
        purpose: formData.purpose,
        nextDate: formData.nextDate,
        participants: formData.participants,
        duration: formData.duration
      };
      onSave(saveSession);
    };
    return (
      <div className="bg-white rounded-lg shadow-xl overflow-hidden">
        <div className="px-6 py-4 border-b border-gray-200 flex justify-between items-center">
          <h3 className="text-lg font-medium text-gray-900">
            {session ? 'Editar Sesión' : 'Nueva Sesión'}
          </h3>
          <button onClick={onCancel} className="text-gray-400 hover:text-gray-500">
            <X className="h-6 w-6" />
          </button>
        </div>
        <form onSubmit={handleSubmit} className="p-6">
          <div className="space-y-4">
            <div>
              <label className="block text-sm font-medium text-gray-700">Tipo de Sesión</label>
              <select 
                name="type" 
                value={formData.type}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              >
                <option value="Internas">Internas</option>
                <option value="Clientes">Clientes</option>
                <option value="Stakeholders">Stakeholders</option>
                <option value="Equipo">Equipo</option>
              </select>
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Frecuencia</label>
              <select 
                name="frequency" 
                value={formData.frequency}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              >
                <option value="Diaria">Diaria</option>
                <option value="Semanal">Semanal</option>
                <option value="Quincenal">Quincenal</option>
                <option value="Mensual">Mensual</option>
              </select>
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Propósito</label>
              <input 
                type="text" 
                name="purpose" 
                value={formData.purpose}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Próxima Fecha</label>
              <input 
                type="date" 
                name="nextDate" 
                value={formData.nextDate}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Participantes</label>
              <input 
                type="text" 
                name="participants" 
                value={formData.participants}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Duración</label>
              <input 
                type="text" 
                name="duration" 
                value={formData.duration}
                onChange={handleChange}
                placeholder="Ej: 1 hora" 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
          </div>
          <div className="mt-6 flex justify-end space-x-3">
            <button 
              type="button" 
              onClick={onCancel}
              className="inline-flex justify-center px-4 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              Cancelar
            </button>
            <button 
              type="submit" 
              className="inline-flex justify-center px-4 py-2 text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 border border-transparent rounded-md hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              {session ? 'Actualizar' : 'Guardar'}
            </button>
          </div>
        </form>
      </div>
    );
  };

  // Session Details Component
  const SessionDetails = ({ session, onClose }) => {
    const sessionTypeColor = session.type === 'Internas' ? 'from-blue-500 to-indigo-600' : 'from-green-500 to-emerald-600';
    return (
      <div className="bg-white rounded-lg shadow-xl overflow-hidden">
        <div className={`px-6 py-4 border-b bg-gradient-to-r ${sessionTypeColor} flex justify-between items-center`}>
          <h3 className="text-lg font-medium text-white">Detalles de la Sesión</h3>
          <button onClick={onClose} className="text-white hover:text-gray-200">
            <X className="h-6 w-6" />
          </button>
        </div>
        <div className="p-6">
          <div className="space-y-4 text-sm">
            <div className="flex justify-between">
              <span className="text-gray-500">Tipo:</span>
              <span className="font-medium">{session.type}</span>
            </div>
            <div className="flex justify-between">
              <span className="text-gray-500">Frecuencia:</span>
              <span className="font-medium">{session.frequency}</span>
            </div>
            <div className="flex justify-between">
              <span className="text-gray-500">Propósito:</span>
              <span className="font-medium">{session.purpose}</span>
            </div>
            <div className="flex justify-between">
              <span className="text-gray-500">Próxima Fecha:</span>
              <span className="font-medium">{session.nextDate}</span>
            </div>
            <div className="flex justify-between">
              <span className="text-gray-500">Participantes:</span>
              <span className="font-medium">{session.participants}</span>
            </div>
            <div className="flex justify-between">
              <span className="text-gray-500">Duración:</span>
              <span className="font-medium">{session.duration}</span>
            </div>
          </div>
          <div className="mt-6 flex justify-end space-x-3">
            <button 
              onClick={() => {
                setEditingSession(session);
                onClose();
              }}
              className="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              <Edit className="h-4 w-4 mr-1" />
              Editar
            </button>
            <button 
              onClick={onClose}
              className="inline-flex justify-center px-3 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              Cerrar
            </button>
          </div>
        </div>
      </div>
    );
  };

  // Assignment Details Component
  const AssignmentDetails = ({ member, onClose }) => {
    const availabilityColor = member.availability >= '70%' ? 'from-green-500 to-emerald-500' : 'from-yellow-500 to-orange-500';
    return (
      <div className="bg-white rounded-lg shadow-xl overflow-hidden">
        <div className="px-6 py-4 border-b border-gray-200 flex justify-between items-center">
          <h3 className="text-lg font-medium text-gray-900">Planeación de {member.name}</h3>
          <button onClick={onClose} className="text-gray-400 hover:text-gray-500">
            <X className="h-6 w-6" />
          </button>
        </div>
        <div className="p-6">
          <div className="flex items-center mb-6">
            <div className="relative">
              <img 
                src={member.avatar} 
                alt={member.name}
                className="h-16 w-16 rounded-full ring-4 ring-white shadow-lg"
              />
              <div className={`absolute -bottom-1 -right-1 h-8 w-8 rounded-full bg-gradient-to-r ${availabilityColor} flex items-center justify-center`}>
                <Users className="h-4 w-4 text-white" />
              </div>
            </div>
            <div className="ml-4">
              <h4 className="text-lg font-bold text-gray-900">{member.name}</h4>
              <p className="text-sm font-medium text-indigo-600">{member.role}</p>
              <div className="mt-1">
                <span className={`inline-flex items-center px-3 py-1 rounded-full text-xs font-medium bg-gradient-to-r ${availabilityColor} text-white`}>
                  Disponibilidad: {member.availability}
                </span>
              </div>
            </div>
          </div>
          <div className="mb-6">
            <h5 className="text-sm font-bold text-gray-900 mb-3">Habilidades</h5>
            <div className="flex flex-wrap gap-2">
              {member.skills.map((skill, index) => (
                <span key={index} className="inline-flex items-center px-3 py-1 rounded-full text-xs font-medium bg-indigo-100 text-indigo-800">
                  {skill}
                </span>
              ))}
            </div>
          </div>
          <div>
            <h5 className="text-sm font-bold text-gray-900 mb-3">Proyectos Asignados</h5>
            <div className="space-y-4">
              {member.projects.map((project, index) => {
                const projectData = projects.find(p => p.id === project.projectId);
                return (
                  <div key={index} className="border border-gray-200 rounded-lg p-4 bg-gradient-to-r from-white to-gray-50">
                    <div className="flex justify-between items-start mb-2">
                      <h6 className="font-bold text-gray-900">{project.projectName}</h6>
                      <span className={`inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium ${getStatusColor(project.status)}`}>
                        {project.status}
                      </span>
                    </div>
                    <div className="flex justify-between text-sm text-gray-500 mb-2">
                      <span>Horas asignadas: {project.hours}h</span>
                      <span>{project.tasks.length} tareas</span>
                    </div>
                    <div className="mt-2">
                      <h6 className="text-xs font-bold text-gray-700 mb-1">Tareas</h6>
                      <ul className="list-disc list-inside space-y-1">
                        {project.tasks.map((task, taskIndex) => (
                          <li key={taskIndex} className="text-sm text-gray-900">{task}</li>
                        ))}
                      </ul>
                    </div>
                    <div className="mt-3 pt-3 border-t border-gray-100">
                      <h6 className="text-xs font-bold text-gray-700 mb-2">Seguimiento del Proyecto</h6>
                      {projectData && (
                        <div className="bg-gray-50 rounded p-3">
                          <div className="flex justify-between items-center mb-1">
                            <span className="text-xs text-gray-600">Avance del proyecto</span>
                            <span className="text-xs font-bold text-gray-900">
                              {projectData.progress}%
                            </span>
                          </div>
                          <div className="w-full bg-gray-200 rounded-full h-2">
                            <div 
                              className={`h-2 rounded-full bg-gradient-to-r ${projectData.color}`} 
                              style={{ width: `${projectData.progress}%` }}
                            ></div>
                          </div>
                        </div>
                      )}
                    </div>
                  </div>
                );
              })}
            </div>
          </div>
          <div className="mt-6 flex justify-end">
            <button 
              onClick={onClose}
              className="inline-flex justify-center px-3 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              Cerrar
            </button>
          </div>
        </div>
      </div>
    );
  };

  // Gantt Chart Component
  const GanttChartView = () => {
    const getDaysBetweenDates = (startDate, endDate) => {
      const start = new Date(startDate);
      const end = new Date(endDate);
      const diffTime = Math.abs(end - start);
      return Math.ceil(diffTime / (1000 * 60 * 60 * 24)) + 1;
    };
    const getDayOffset = (startDate, targetDate) => {
      const start = new Date(startDate);
      const target = new Date(targetDate);
      const diffTime = target - start;
      return Math.ceil(diffTime / (1000 * 60 * 60 * 24));
    };
    let earliestStart = '2024-11-20';
    let latestEnd = '2025-05-20';
    projects.forEach(project => {
      if (project.startDate < earliestStart) earliestStart = project.startDate;
      if (project.endDate > latestEnd) latestEnd = project.endDate;
    });
    const totalDays = getDaysBetweenDates(earliestStart, latestEnd);
    const dateHeaders = [];
    const startDate = new Date(earliestStart);
    for (let i = 0; i < totalDays; i += 7) {
      const currentDate = new Date(startDate);
      currentDate.setDate(startDate.getDate() + i);
      dateHeaders.push(currentDate.toISOString().split('T')[0]);
    }
    return (
      <div className="bg-white shadow rounded-lg overflow-hidden">
        <div className="px-6 py-4 border-b border-gray-200">
          <h3 className="text-lg font-medium text-gray-900">Diagrama de Gantt</h3>
          <p className="mt-1 text-sm text-gray-500">Visualización de la planificación y progreso de los proyectos</p>
        </div>
        <div className="overflow-x-auto">
          <div className="p-6">
            <div className="flex mb-4 border-b border-gray-200 pb-2">
              <div className="w-64 font-medium text-gray-700">Tarea/Proyecto</div>
              <div className="flex-1 relative">
                <div className="flex" style={{ width: `${totalDays * 20}px` }}>
                  {dateHeaders.map((date, index) => (
                    <div 
                      key={date} 
                      className="text-xs text-gray-500 border-r border-gray-100 px-2"
                      style={{ width: `${7 * 20}px` }}
                    >
                      {new Date(date).toLocaleDateString('es-ES', { month: 'short', day: 'numeric' })}
                    </div>
                  ))}
                </div>
              </div>
            </div>
            {projects.map(project => (
              <div key={project.id} className="mb-6">
                <div className="flex items-center mb-2">
                  <div className="w-64 font-bold text-gray-900">
                    <div className={`inline-block w-3 h-3 rounded-full mr-2 bg-gradient-to-r ${project.color}`}></div>
                    {project.name}
                  </div>
                  <div className="flex-1">
                    <div className="w-full bg-gray-200 rounded-full h-2">
                      <div 
                        className={`h-2 rounded-full bg-gradient-to-r ${project.color}`} 
                        style={{ width: `${project.progress}%` }}
                      ></div>
                    </div>
                  </div>
                </div>
                {project.tasks.map(task => {
                  const taskStartOffset = getDayOffset(earliestStart, task.start);
                  const taskDuration = getDaysBetweenDates(task.start, task.end);
                  let taskColor = 'from-gray-400 to-gray-500';
                  if (task.status === 'Completado') {
                    taskColor = 'from-green-500 to-green-600';
                  } else if (task.status === 'En Progreso') {
                    taskColor = 'from-yellow-500 to-orange-500';
                  } else if (task.status === 'Pendiente') {
                    taskColor = 'from-gray-300 to-gray-400';
                  }
                  return (
                    <div key={task.id} className="flex items-center mb-1">
                      <div className="w-64 pl-4 text-sm text-gray-600">{task.name}</div>
                      <div className="flex-1 relative" style={{ height: '24px' }}>
                        <div 
                          className="absolute top-1/2 transform -translate-y-1/2 rounded"
                          style={{ 
                            left: `${taskStartOffset * 20}px`, 
                            width: `${taskDuration * 20}px`,
                            height: '12px',
                            background: `linear-gradient(to right, ${taskColor.split(' ')[0].replace('from-', '#').replace('-', '')} 0%, ${taskColor.split(' ')[1].replace('to-', '#').replace('-', '')} 100%)`
                          }}
                        >
                          <div 
                            className={`h-full rounded ${getProgressColor(task.progress)}`}
                            style={{ width: `${task.progress}%` }}
                          ></div>
                        </div>
                        <div 
                          className="absolute top-1/2 transform -translate-y-1/2 text-xs text-gray-500 font-bold"
                          style={{ left: `${taskStartOffset * 20}px` }}
                        >
                          {task.progress}%
                        </div>
                      </div>
                    </div>
                  );
                })}
              </div>
            ))}
          </div>
        </div>
        <div className="px-6 py-4 bg-gray-50 border-t border-gray-200">
          <div className="flex flex-wrap gap-4">
            <div className="flex items-center">
              <div className="w-3 h-3 from-blue-500 to-indigo-600 rounded mr-2" style={{background: 'linear-gradient(to right, #3b82f6, #4f46e5)'}}></div>
              <span className="text-xs text-gray-600">Proyecto Efecty</span>
            </div>
            <div className="flex items-center">
              <div className="w-3 h-3 from-green-500 to-emerald-600 rounded mr-2" style={{background: 'linear-gradient(to right, #10b981, #059669)'}}></div>
              <span className="text-xs text-gray-600">Aseguradora Solidaria</span>
            </div>
            <div className="flex items-center">
              <div className="w-3 h-3 from-purple-500 to-pink-600 rounded mr-2" style={{background: 'linear-gradient(to right, #8b5cf6, #db2777)'}}></div>
              <span className="text-xs text-gray-600">Digital Transformation</span>
            </div>
            <div className="flex items-center">
              <div className="w-3 h-3 bg-green-500 rounded mr-2"></div>
              <span className="text-xs text-gray-600">Completado</span>
            </div>
            <div className="flex items-center">
              <div className="w-3 h-3 bg-yellow-500 rounded mr-2"></div>
              <span className="text-xs text-gray-600">En Progreso</span>
            </div>
            <div className="flex items-center">
              <div className="w-3 h-3 bg-red-500 rounded mr-2"></div>
              <span className="text-xs text-gray-600">Retrasado</span>
            </div>
          </div>
        </div>
      </div>
    );
  };

  // Enhanced colorful assignment card
  const ColorfulAssignmentCard = ({ member, onViewDetails }) => {
    const totalHours = member.projects.reduce((sum, project) => sum + project.hours, 0);
    const projectsCount = member.projects.length;
    const availabilityColor = member.availability >= '70%' ? 'from-green-500 to-emerald-500' : 'from-yellow-500 to-orange-500';
    return (
      <div className="bg-white rounded-xl shadow-lg overflow-hidden hover:shadow-xl transition-all duration-300">
        <div className="p-6">
          <div className="flex items-center mb-4">
            <div className="relative">
              <img 
                src={member.avatar} 
                alt={member.name}
                className="h-16 w-16 rounded-full ring-4 ring-white shadow-lg"
              />
              <div className={`absolute -bottom-1 -right-1 h-6 w-6 rounded-full bg-gradient-to-r ${availabilityColor} flex items-center justify-center`}>
                <Users className="h-3 w-3 text-white" />
              </div>
            </div>
            <div className="ml-4">
              <h3 className="text-lg font-bold text-gray-900">{member.name}</h3>
              <p className="text-sm font-medium text-indigo-600">{member.role}</p>
            </div>
          </div>
          <div className="space-y-3">
            <div className="flex justify-between items-center">
              <span className="text-sm text-gray-600 font-medium">Horas asignadas</span>
              <span className="text-sm font-bold text-blue-600">{totalHours}h</span>
            </div>
            <div className="flex justify-between items-center">
              <span className="text-sm text-gray-600 font-medium">Proyectos</span>
              <span className="text-sm font-bold text-purple-600">{projectsCount}</span>
            </div>
            <div className="flex justify-between items-center">
              <span className="text-sm text-gray-600 font-medium">Disponibilidad</span>
              <span className={`text-sm font-bold bg-gradient-to-r ${availabilityColor} bg-clip-text text-transparent`}>
                {member.availability}
              </span>
            </div>
          </div>
          <div className="mt-4">
            <h4 className="text-sm font-bold text-gray-900 mb-2">Proyectos actuales</h4>
            <div className="space-y-2">
              {member.projects.map((project, index) => {
                const projectData = projects.find(p => p.id === project.projectId);
                return (
                  <div key={index} className="flex items-center justify-between p-2 bg-gray-50 rounded-lg">
                    <div>
                      <div className="text-sm font-medium text-gray-900">{project.projectName}</div>
                      <div className="text-xs text-gray-500">{project.status}</div>
                    </div>
                    <div className={`h-2 w-16 rounded-full bg-gradient-to-r ${projectData?.color || 'from-gray-400 to-gray-500'}`}>
                      <div className="h-2 rounded-full bg-white bg-opacity-30" style={{ width: `${project.hours * 4}%` }}></div>
                    </div>
                  </div>
                );
              })}
            </div>
          </div>
          <div className="mt-4 pt-4 border-t border-gray-100 flex space-x-2">
            <button 
              onClick={() => onViewDetails(member)}
              className="flex-1 inline-flex items-center justify-center px-3 py-1.5 border border-gray-300 rounded-lg text-sm font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 transition-colors duration-200"
            >
              <Eye className="h-4 w-4 mr-1" />
              Ver
            </button>
            <button 
              onClick={() => setEditingMember(member)}
              className="inline-flex items-center px-3 py-1.5 border border-transparent rounded-lg text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 transition-all duration-200"
            >
              <Edit className="h-4 w-4 mr-1" />
              Editar
            </button>
            <button 
              onClick={() => deleteMember(member.id)}
              className="inline-flex items-center px-3 py-1.5 border border-transparent rounded-lg text-sm font-medium text-white bg-gradient-to-r from-red-600 to-orange-600 hover:from-red-700 hover:to-orange-700 focus:outline-none focus:ring-2 focus:ring-offset-2 transition-all duration-200"
            >
              <Trash2 className="h-4 w-4 mr-1" />
              Eliminar
            </button>
          </div>
        </div>
      </div>
    );
  };

  // Member Form Component
  const MemberForm = ({ member, onSave, onCancel }) => {
    const initialFormData = {
      name: member?.name || '',
      role: member?.role || '',
      availability: member?.availability || '80%',
      skills: member?.skills?.join(', ') || '',
      projects: member?.projects || []
    };
    const [formData, setFormData] = useState(initialFormData);
    
    useEffect(() => {
      if (member) {
        setFormData({
          name: member.name || '',
          role: member.role || '',
          availability: member.availability || '80%',
          skills: member.skills?.join(', ') || '',
          projects: member.projects || []
        });
      } else {
        setFormData(initialFormData);
      }
    }, [member]);

    const handleChange = (e) => {
      setFormData({
        ...formData,
        [e.target.name]: e.target.value
      });
    };

    const handleProjectChange = (projectId, field, value) => {
      const updatedProjects = formData.projects.map(proj => 
        proj.projectId === projectId ? { ...proj, [field]: value } : proj
      );
      setFormData({ ...formData, projects: updatedProjects });
    };

    const toggleProjectAssignment = (projectId) => {
      const projectExists = formData.projects.some(p => p.projectId === projectId);
      if (projectExists) {
        const updatedProjects = formData.projects.filter(p => p.projectId !== projectId);
        setFormData({ ...formData, projects: updatedProjects });
      } else {
        const project = projects.find(p => p.id === projectId);
        if (project) {
          const newProjectAssignment = {
            projectId: project.id,
            projectName: project.name,
            hours: 0,
            tasks: [],
            status: project.status
          };
          setFormData({ 
            ...formData, 
            projects: [...formData.projects, newProjectAssignment] 
          });
        }
      }
    };

    const handleSubmit = (e) => {
      e.preventDefault();
      const updatedMember = {
        id: member?.id || null,
        name: formData.name,
        role: formData.role,
        availability: formData.availability,
        skills: formData.skills.split(',').map(s => s.trim()).filter(s => s),
        projects: formData.projects
      };
      onSave(updatedMember);
    };

    return (
      <div className="bg-white rounded-lg shadow-xl overflow-hidden">
        <div className="px-6 py-4 border-b border-gray-200 flex justify-between items-center">
          <h3 className="text-lg font-medium text-gray-900">
            {member ? 'Editar Miembro' : 'Nuevo Miembro'}
          </h3>
          <button onClick={onCancel} className="text-gray-400 hover:text-gray-500">
            <X className="h-6 w-6" />
          </button>
        </div>
        <form onSubmit={handleSubmit} className="p-6">
          <div className="space-y-4">
            <div>
              <label className="block text-sm font-medium text-gray-700">Nombre Completo</label>
              <input 
                type="text" 
                name="name" 
                value={formData.name}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Rol</label>
              <input 
                type="text" 
                name="role" 
                value={formData.role}
                onChange={handleChange}
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Disponibilidad (%)</label>
              <input 
                type="number" 
                name="availability" 
                value={formData.availability.replace('%', '')}
                onChange={(e) => setFormData({...formData, availability: e.target.value + '%'})}
                min="0" 
                max="100" 
                required 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              />
            </div>
            <div>
              <label className="block text-sm font-medium text-gray-700">Habilidades (separadas por comas)</label>
              <textarea 
                name="skills" 
                value={formData.skills}
                onChange={handleChange}
                rows="2" 
                className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
              ></textarea>
            </div>
            
            {/* Project Assignments */}
            <div className="mt-6">
              <h4 className="text-sm font-medium text-gray-900 mb-3">Asignación de Proyectos</h4>
              <div className="space-y-3">
                {projects.map(project => {
                  const isAssigned = formData.projects.some(p => p.projectId === project.id);
                  const projectAssignment = formData.projects.find(p => p.projectId === project.id);
                  return (
                    <div key={project.id} className="border border-gray-200 rounded-lg p-3">
                      <div className="flex items-center justify-between">
                        <div className="flex items-center">
                          <input
                            type="checkbox"
                            checked={isAssigned}
                            onChange={() => toggleProjectAssignment(project.id)}
                            className="h-4 w-4 text-indigo-600 rounded focus:ring-indigo-500"
                          />
                          <label className="ml-3 block text-sm font-medium text-gray-900">
                            {project.name}
                          </label>
                        </div>
                        {isAssigned && (
                          <span className={`inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium ${getStatusColor(project.status)}`}>
                            {projectAssignment?.status || project.status}
                          </span>
                        )}
                      </div>
                      
                      {isAssigned && (
                        <div className="mt-3 space-y-3 pl-7">
                          <div>
                            <label className="block text-xs font-medium text-gray-700">Horas asignadas</label>
                            <input 
                              type="number" 
                              value={projectAssignment?.hours || 0}
                              onChange={(e) => handleProjectChange(project.id, 'hours', parseInt(e.target.value) || 0)}
                              min="0"
                              className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-1 px-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 text-sm"
                            />
                          </div>
                          <div>
                            <label className="block text-xs font-medium text-gray-700">Tareas (una por línea)</label>
                            <textarea 
                              value={projectAssignment?.tasks?.join('\n') || ''}
                              onChange={(e) => handleProjectChange(project.id, 'tasks', e.target.value.split('\n').filter(t => t.trim() !== ''))}
                              rows="2"
                              className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-1 px-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 text-sm"
                            ></textarea>
                          </div>
                          <div>
                            <label className="block text-xs font-medium text-gray-700">Estado en el proyecto</label>
                            <select 
                              value={projectAssignment?.status || project.status}
                              onChange={(e) => handleProjectChange(project.id, 'status', e.target.value)}
                              className="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-1 px-2 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 text-sm"
                            >
                              <option value="Planeación">Planeación</option>
                              <option value="En Progreso">En Progreso</option>
                              <option value="Completado">Completado</option>
                              <option value="Retrasado">Retrasado</option>
                              <option value="Pendiente">Pendiente</option>
                            </select>
                          </div>
                        </div>
                      )}
                    </div>
                  );
                })}
              </div>
            </div>
          </div>
          <div className="mt-6 flex justify-end space-x-3">
            <button 
              type="button" 
              onClick={onCancel}
              className="inline-flex justify-center px-4 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              Cancelar
            </button>
            <button 
              type="submit" 
              className="inline-flex justify-center px-4 py-2 text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 border border-transparent rounded-md hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
            >
              {member ? 'Actualizar' : 'Guardar'}
            </button>
          </div>
        </form>
      </div>
    );
  };

  const addMember = (newMember) => {
    const newId = Math.max(...teamMembers.map(m => m.id), 0) + 1;
    const avatarInitials = newMember.name.split(' ').map(n => n[0]).join('').toUpperCase();
    const colors = ['3b82f6', 'ef4444', '10b981', 'f59e0b', '8b5cf6', 'ec4899', '06b6d4'];
    const randomColor = colors[Math.floor(Math.random() * colors.length)];
    const avatar = `https://placehold.co/40x40/${randomColor}/ffffff?text=${avatarInitials}`;
    
    setTeamMembers([...teamMembers, { ...newMember, id: newId, avatar }]);
    setShowAddMember(false);
  };

  const updateMember = (updatedMember) => {
    setTeamMembers(teamMembers.map(m => 
      m.id === updatedMember.id ? updatedMember : m
    ));
    setEditingMember(null);
  };

  const deleteMember = (id) => {
    if (window.confirm('¿Está seguro de eliminar este miembro del equipo?')) {
      setTeamMembers(teamMembers.filter(m => m.id !== id));
    }
  };

  const [editingMember, setEditingMember] = useState(null);
  const [showAddMember, setShowAddMember] = useState(false);

  return (
    <div className="min-h-screen bg-gradient-to-br from-gray-50 to-gray-100">
      {/* Header */}
      <header className="bg-white shadow-sm border-b">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
          <div className="flex items-center justify-between">
            <div>
              <h1 className="text-3xl font-bold text-gray-900">Dashboard de Gestión de Proyectos</h1>
              <p className="mt-1 text-sm text-gray-600">Visibilidad completa de todos los proyectos, sesiones y asignaciones</p>
            </div>
            <button 
              onClick={() => setShowAddProject(true)}
              className="inline-flex items-center px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-all duration-200"
            >
              <Plus className="h-5 w-5 mr-2" />
              Nuevo Proyecto
            </button>
          </div>
        </div>
      </header>
      {/* Navigation Tabs */}
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-6">
        <nav className="flex space-x-6 xl:space-x-8 border-b border-gray-200">
          <button
            onClick={() => setActiveTab('overview')}
            className={`py-4 px-1 border-b-2 font-medium text-sm whitespace-nowrap focus:outline-none ${
              activeTab === 'overview' 
                ? 'border-indigo-500 text-indigo-600' 
                : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'
            }`}
          >
            Visibilidad General
          </button>
          <button
            onClick={() => setActiveTab('projects')}
            className={`py-4 px-1 border-b-2 font-medium text-sm whitespace-nowrap focus:outline-none ${
              activeTab === 'projects' 
                ? 'border-indigo-500 text-indigo-600' 
                : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'
            }`}
          >
            Proyectos Detallados
          </button>
          <button
            onClick={() => setActiveTab('sessions')}
            className={`py-4 px-1 border-b-2 font-medium text-sm whitespace-nowrap focus:outline-none ${
              activeTab === 'sessions' 
                ? 'border-indigo-500 text-indigo-600' 
                : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'
            }`}
          >
            Sesiones de Seguimiento
          </button>
          <button
            onClick={() => setActiveTab('assignments')}
            className={`py-4 px-1 border-b-2 font-medium text-sm whitespace-nowrap focus:outline-none ${
              activeTab === 'assignments' 
                ? 'border-indigo-500 text-indigo-600' 
                : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'
            }`}
          >
            Asignaciones y Planeación
          </button>
          <button
            onClick={() => setActiveTab('analytics')}
            className={`py-4 px-1 border-b-2 font-medium text-sm whitespace-nowrap focus:outline-none ${
              activeTab === 'analytics' 
                ? 'border-indigo-500 text-indigo-600' 
                : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'
            }`}
          >
            <BarChart2 className="h-4 w-4 inline mr-1" />
            Dashboards Analíticos
          </button>
          <button
            onClick={() => setActiveTab('gantt')}
            className={`py-4 px-1 border-b-2 font-medium text-sm whitespace-nowrap focus:outline-none ${
              activeTab === 'gantt' 
                ? 'border-indigo-500 text-indigo-600' 
                : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'
            }`}
          >
            <GanttChart className="h-4 w-4 inline mr-1" />
            Diagrama de Gantt
          </button>
        </nav>
      </div>
      {/* Main Content */}
      <main className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        {/* Overview Tab */}
        {activeTab === 'overview' && (
          <div className="space-y-8">
            {/* Key Metrics */}
            <div className="grid grid-cols-1 md:grid-cols-4 gap-6">
              <div className="bg-gradient-to-r from-blue-500 to-indigo-600 rounded-xl shadow-lg p-6 text-white">
                <div className="flex items-center">
                  <div className="flex-shrink-0">
                    <Users className="h-8 w-8 text-blue-100" />
                  </div>
                  <div className="ml-5 w-0 flex-1">
                    <dl>
                      <dt className="text-sm font-medium text-blue-100 truncate">Capacidad del Equipo</dt>
                      <dd className="text-2xl font-bold">{projects.reduce((sum, p) => sum + parseInt(p.teamCapacity), 0) / projects.length}%</dd>
                    </dl>
                  </div>
                </div>
              </div>
              <div className="bg-gradient-to-r from-green-500 to-emerald-600 rounded-xl shadow-lg p-6 text-white">
                <div className="flex items-center">
                  <div className="flex-shrink-0">
                    <BarChart2 className="h-8 w-8 text-green-100" />
                  </div>
                  <div className="ml-5 w-0 flex-1">
                    <dl>
                      <dt className="text-sm font-medium text-green-100 truncate">Avance Promedio</dt>
                      <dd className="text-2xl font-bold">{Math.round(projects.reduce((sum, p) => sum + p.progress, 0) / projects.length)}%</dd>
                    </dl>
                  </div>
                </div>
              </div>
              <div className="bg-gradient-to-r from-yellow-500 to-orange-600 rounded-xl shadow-lg p-6 text-white">
                <div className="flex items-center">
                  <div className="flex-shrink-0">
                    <AlertTriangle className="h-8 w-8 text-yellow-100" />
                  </div>
                  <div className="ml-5 w-0 flex-1">
                    <dl>
                      <dt className="text-sm font-medium text-yellow-100 truncate">Bloqueadores</dt>
                      <dd className="text-2xl font-bold">
                        {projects.reduce((sum, p) => sum + p.stoppers.length, 0)}
                      </dd>
                    </dl>
                  </div>
                </div>
              </div>
              <div className="bg-gradient-to-r from-purple-500 to-pink-600 rounded-xl shadow-lg p-6 text-white">
                <div className="flex items-center">
                  <div className="flex-shrink-0">
                    <User className="h-8 w-8 text-purple-100" />
                  </div>
                  <div className="ml-5 w-0 flex-1">
                    <dl>
                      <dt className="text-sm font-medium text-purple-100 truncate">Miembros del Equipo</dt>
                      <dd className="text-2xl font-bold">{teamMembers.length}</dd>
                    </dl>
                  </div>
                </div>
              </div>
            </div>
            {/* Projects Summary */}
            <div className="bg-white shadow rounded-lg">
              <div className="px-4 py-5 sm:px-6">
                <h3 className="text-lg leading-6 font-medium text-gray-900">Resumen de Proyectos</h3>
                <p className="mt-1 max-w-2xl text-sm text-gray-500">Visibilidad general de todos los proyectos activos</p>
              </div>
              <div className="border-t border-gray-200 p-6">
                <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                  {projects.map(project => (
                    <div key={project.id} className="hover:bg-gray-50 transition-colors duration-200">
                      <ColorfulProjectCard 
                        project={project}
                        onView={setSelectedProject}
                        onEdit={setEditingProject}
                        onDelete={deleteProject}
                      />
                    </div>
                  ))}
                </div>
              </div>
            </div>
            {/* Upcoming Sessions */}
            <div className="bg-white shadow rounded-lg">
              <div className="px-4 py-5 sm:px-6">
                <h3 className="text-lg leading-6 font-medium text-gray-900">Próximas Sesiones</h3>
                <p className="mt-1 max-w-2xl text-sm text-gray-500">Seguimiento programado para los próximos 30 días</p>
              </div>
              <div className="border-t border-gray-200">
                <ul className="divide-y divide-gray-200">
                  {sessions.map(session => (
                    <li key={session.id} className="hover:bg-gray-50">
                      <div className="px-4 py-4 sm:px-6">
                        <div className="flex items-center justify-between">
                          <div className="flex items-center">
                            <div className={`h-10 w-10 rounded-full flex items-center justify-center ${
                              session.type === 'Internas' 
                                ? 'bg-gradient-to-r from-blue-500 to-indigo-600 text-white' 
                                : 'bg-gradient-to-r from-green-500 to-emerald-600 text-white'
                            }`}>
                              <MessageSquare className="h-5 w-5" />
                            </div>
                            <div className="ml-4">
                              <div className="text-sm font-medium text-gray-900">{session.type}</div>
                              <div className="text-sm text-gray-500">Frecuencia: {session.frequency}</div>
                            </div>
                          </div>
                          <div className="ml-4 flex-shrink-0">
                            <span className="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-gradient-to-r from-purple-500 to-pink-600 text-white">
                              {session.nextDate}
                            </span>
                          </div>
                        </div>
                        <div className="mt-2 sm:flex sm:justify-between">
                          <div className="sm:w-1/2">
                            <div className="text-sm text-gray-500">
                              <strong>Propósito:</strong> {session.purpose}
                            </div>
                          </div>
                          <div className="mt-2 sm:mt-0 sm:w-1/2">
                            <div className="text-sm text-gray-500">
                              <strong>Participantes:</strong> {session.participants}
                            </div>
                          </div>
                        </div>
                        <div className="mt-4 flex justify-end space-x-2">
                          <button 
                            onClick={() => setEditingSession(session)}
                            className="inline-flex items-center px-3 py-1 border border-gray-300 shadow-sm text-xs font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                          >
                            <Edit className="h-3 w-3 mr-1" />
                            Editar
                          </button>
                          <button 
                            onClick={() => deleteSession(session.id)}
                            className="inline-flex items-center px-3 py-1 border border-gray-300 shadow-sm text-xs font-medium rounded-md text-red-700 bg-white hover:bg-red-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500"
                          >
                            <Trash2 className="h-3 w-3 mr-1" />
                            Eliminar
                          </button>
                        </div>
                      </div>
                    </li>
                  ))}
                </ul>
              </div>
            </div>
          </div>
        )}
        {/* Projects Tab */}
        {activeTab === 'projects' && (
          <div className="space-y-6">
            <div className="flex justify-between items-center">
              <h2 className="text-2xl font-bold text-gray-900">Proyectos Detallados</h2>
              <button 
                onClick={() => setShowAddProject(true)}
                className="inline-flex items-center px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
              >
                <Plus className="h-5 w-5 mr-2" />
                Nuevo Proyecto
              </button>
            </div>
            <div className="grid grid-cols-1 gap-6">
              {projects.map(project => (
                <ColorfulProjectCard 
                  key={project.id}
                  project={project}
                  onView={setSelectedProject}
                  onEdit={setEditingProject}
                  onDelete={deleteProject}
                />
              ))}
            </div>
          </div>
        )}
        {/* Sessions Tab */}
        {activeTab === 'sessions' && (
          <div className="space-y-6">
            <div className="flex justify-between items-center">
              <h2 className="text-2xl font-bold text-gray-900">Sesiones de Seguimiento</h2>
              <button 
                onClick={() => setShowAddSession(true)}
                className="inline-flex items-center px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
              >
                <Plus className="h-5 w-5 mr-2" />
                Nueva Sesión
              </button>
            </div>
            <div className="grid grid-cols-1 gap-6">
              {sessions.map(session => (
                <div key={session.id} className="bg-white shadow rounded-lg overflow-hidden hover:shadow-lg transition-shadow duration-200">
                  <div className={`px-4 py-5 sm:px-6 border-b ${
                    session.type === 'Internas' 
                      ? 'bg-gradient-to-r from-blue-50 to-indigo-50' 
                      : 'bg-gradient-to-r from-green-50 to-emerald-50'
                  }`}>
                    <div className="flex items-center justify-between">
                      <div>
                        <h3 className="text-lg font-medium text-gray-900">{session.type} - {session.purpose}</h3>
                        <p className="mt-1 text-sm text-gray-500">Frecuencia: {session.frequency}</p>
                      </div>
                      <div className="flex items-center space-x-2">
                        <span className="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-gradient-to-r from-purple-500 to-pink-600 text-white">
                          {session.nextDate}
                        </span>
                        <button 
                          onClick={() => setEditingSession(session)}
                          className="inline-flex items-center px-3 py-1 border border-gray-300 shadow-sm text-sm leading-4 font-medium rounded-md text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                        >
                          <Edit className="h-4 w-4 mr-1" />
                          Editar
                        </button>
                        <button 
                          onClick={() => deleteSession(session.id)}
                          className="inline-flex items-center px-3 py-1 border border-gray-300 shadow-sm text-sm leading-4 font-medium rounded-md text-red-700 bg-white hover:bg-red-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500"
                        >
                          <Trash2 className="h-4 w-4 mr-1" />
                          Eliminar
                        </button>
                      </div>
                    </div>
                  </div>
                  <div className="px-4 py-5 sm:p-6">
                    <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                      <div>
                        <h4 className="text-sm font-medium text-gray-900 mb-2">Participantes</h4>
                        <p className="text-sm text-gray-900">{session.participants}</p>
                      </div>
                      <div>
                        <h4 className="text-sm font-medium text-gray-900 mb-2">Duración</h4>
                        <p className="text-sm text-gray-900">{session.duration}</p>
                      </div>
                    </div>
                    <div className="mt-6">
                      <h4 className="text-sm font-medium text-gray-900 mb-2">Objetivo</h4>
                      <p className="text-sm text-gray-900">{session.purpose}</p>
                    </div>
                    <div className="mt-6">
                      <h4 className="text-sm font-medium text-gray-900 mb-2">Notas Adicionales</h4>
                      <p className="text-sm text-gray-900">
                        Las sesiones deben documentarse con actas y seguimiento de acciones.
                        Se recomienda enviar recordatorios 24 horas antes de la reunión.
                      </p>
                    </div>
                  </div>
                </div>
              ))}
            </div>
          </div>
        )}
        {/* Assignments Tab */}
        {activeTab === 'assignments' && (
          <div className="space-y-6">
            <div className="flex justify-between items-center">
              <h2 className="text-2xl font-bold text-gray-900">Asignaciones y Planeación</h2>
              <div className="flex items-center space-x-3">
                <button
                  onClick={() => setShowAddMember(true)}
                  className="inline-flex items-center px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
                >
                  <Plus className="h-5 w-5 mr-2" />
                  Agregar Miembro
                </button>
                <div className="flex bg-gray-100 rounded-md p-1">
                  <button
                    onClick={() => setAssignmentsView('grid')}
                    className={`p-2 rounded-md ${assignmentsView === 'grid' ? 'bg-white shadow-sm text-indigo-600' : 'text-gray-500 hover:text-gray-700'}`}
                  >
                    <Grid className="h-4 w-4" />
                  </button>
                  <button
                    onClick={() => setAssignmentsView('list')}
                    className={`p-2 rounded-md ${assignmentsView === 'list' ? 'bg-white shadow-sm text-indigo-600' : 'text-gray-500 hover:text-gray-700'}`}
                  >
                    <List className="h-4 w-4" />
                  </button>
                </div>
              </div>
            </div>
            {/* Team Summary */}
            <div className="bg-white shadow rounded-lg p-6">
              <div className="grid grid-cols-1 md:grid-cols-4 gap-6">
                <div className="text-center">
                  <div className="text-2xl font-bold text-gray-900">{teamMembers.length}</div>
                  <div className="text-sm text-gray-500">Miembros del equipo</div>
                </div>
                <div className="text-center">
                  <div className="text-2xl font-bold text-gray-900">
                    {teamMembers.reduce((sum, member) => sum + member.projects.length, 0)}
                  </div>
                  <div className="text-sm text-gray-500">Asignaciones totales</div>
                </div>
                <div className="text-center">
                  <div className="text-2xl font-bold text-gray-900">
                    {Math.round(teamMembers.reduce((sum, member) => sum + (100 - parseInt(member.availability)), 0) / teamMembers.length)}%
                  </div>
                  <div className="text-sm text-gray-500">Capacidad utilizada</div>
                </div>
                <div className="text-center">
                  <div className="text-2xl font-bold text-gray-900">
                    {teamMembers.reduce((sum, member) => sum + member.projects.reduce((pSum, proj) => pSum + proj.hours, 0), 0)}
                  </div>
                  <div className="text-sm text-gray-500">Horas asignadas</div>
                </div>
              </div>
            </div>
            {/* Assignments View */}
            {assignmentsView === 'grid' ? (
              <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                {teamMembers.map(member => (
                  <ColorfulAssignmentCard 
                    key={member.id} 
                    member={member} 
                    onViewDetails={setSelectedMember} 
                  />
                ))}
              </div>
            ) : (
              <div className="bg-white shadow rounded-lg overflow-hidden">
                <div className="overflow-x-auto">
                  <table className="min-w-full divide-y divide-gray-200">
                    <thead className="bg-gray-50">
                      <tr>
                        <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Miembro</th>
                        <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Rol</th>
                        <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Proyectos</th>
                        <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Horas</th>
                        <th className="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Disponibilidad</th>
                        <th className="px-6 py-3 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">Acciones</th>
                      </tr>
                    </thead>
                    <tbody className="bg-white divide-y divide-gray-200">
                      {teamMembers.map(member => {
                        const totalHours = member.projects.reduce((sum, project) => sum + project.hours, 0);
                        const availabilityColor = member.availability >= '70%' ? 'text-green-600' : 'text-yellow-600';
                        return (
                          <tr key={member.id} className="hover:bg-gray-50">
                            <td className="px-6 py-4 whitespace-nowrap">
                              <div className="flex items-center">
                                <div className="flex-shrink-0 h-10 w-10">
                                  <img className="h-10 w-10 rounded-full" src={member.avatar} alt={member.name} />
                                </div>
                                <div className="ml-4">
                                  <div className="text-sm font-medium text-gray-900">{member.name}</div>
                                </div>
                              </div>
                            </td>
                            <td className="px-6 py-4 whitespace-nowrap text-sm text-indigo-600 font-medium">{member.role}</td>
                            <td className="px-6 py-4 whitespace-nowrap">
                              <div className="text-sm text-gray-900">
                                {member.projects.map((proj, idx) => (
                                  <div key={idx} className="mb-1 last:mb-0">
                                    <span className="font-medium">{proj.projectName}</span>
                                    <span className={`ml-2 px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${getStatusColor(proj.status)}`}>
                                      {proj.status}
                                    </span>
                                  </div>
                                ))}
                              </div>
                            </td>
                            <td className="px-6 py-4 whitespace-nowrap text-sm font-bold text-blue-600">{totalHours}h</td>
                            <td className="px-6 py-4 whitespace-nowrap">
                              <span className={`px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${availabilityColor}`}>
                                {member.availability}
                              </span>
                            </td>
                            <td className="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                              <button 
                                onClick={() => setSelectedMember(member)}
                                className="text-indigo-600 hover:text-indigo-900 font-medium mr-3"
                              >
                                Ver
                              </button>
                              <button 
                                onClick={() => setEditingMember(member)}
                                className="text-indigo-600 hover:text-indigo-900 font-medium mr-3"
                              >
                                Editar
                              </button>
                              <button 
                                onClick={() => deleteMember(member.id)}
                                className="text-red-600 hover:text-red-900 font-medium"
                              >
                                Eliminar
                              </button>
                            </td>
                          </tr>
                        );
                      })}
                    </tbody>
                  </table>
                </div>
              </div>
            )}
            {/* Project Connection Section */}
            <div className="bg-white shadow rounded-lg p-6">
              <h3 className="text-lg font-medium text-gray-900 mb-4">Conexión con Proyectos</h3>
              <p className="text-sm text-gray-600 mb-4">
                Cada asignación está conectada directamente con las tarjetas de seguimiento de proyectos. 
                Al revisar la planeación de un miembro del equipo, puedes ver el estado actual de los proyectos 
                a los que está asignado y su progreso individual.
              </p>
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                {projects.map(project => {
                  const assignedMembers = teamMembers.filter(member => 
                    member.projects.some(proj => proj.projectId === project.id)
                  );
                  return (
                    <div key={project.id} className="border border-gray-200 rounded-lg p-4 bg-gradient-to-r from-white to-gray-50">
                      <div className="flex justify-between items-start mb-2">
                        <h4 className="font-bold text-gray-900">{project.name}</h4>
                        <span className={`inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium ${getStatusColor(project.status)}`}>
                          {project.status}
                        </span>
                      </div>
                      <div className="mb-3">
                        <div className="flex justify-between items-center mb-1">
                          <span className="text-xs text-gray-600">Avance del proyecto</span>
                          <span className="text-xs font-bold text-gray-900">{project.progress}%</span>
                        </div>
                        <div className="w-full bg-gray-200 rounded-full h-2">
                          <div 
                            className={`h-2 rounded-full bg-gradient-to-r ${project.color}`} 
                            style={{ width: `${project.progress}%` }}
                          ></div>
                        </div>
                      </div>
                      <div>
                        <h5 className="text-xs font-bold text-gray-700 mb-2">Miembros asignados ({assignedMembers.length})</h5>
                        <div className="flex flex-wrap gap-2">
                          {assignedMembers.map(member => (
                            <div key={member.id} className="flex items-center text-xs">
                              <img className="h-6 w-6 rounded-full mr-1" src={member.avatar} alt={member.name} />
                              <span className="font-medium">{member.name}</span>
                            </div>
                          ))}
                        </div>
                      </div>
                    </div>
                  );
                })}
              </div>
            </div>
          </div>
        )}
        {/* Analytics Tab */}
        {activeTab === 'analytics' && <AnalyticsDashboard />}
        {/* Gantt Tab */}
        {activeTab === 'gantt' && (
          <div className="space-y-6">
            <div className="flex justify-between items-center">
              <h2 className="text-2xl font-bold text-gray-900">Diagrama de Gantt</h2>
              <div className="text-sm text-gray-600">
                Rango de fechas: {new Date('2024-11-20').toLocaleDateString('es-ES')} - {new Date('2025-05-20').toLocaleDateString('es-ES')}
              </div>
            </div>
            <GanttChartView />
            <div className="bg-white shadow rounded-lg p-6">
              <h3 className="text-lg font-medium text-gray-900 mb-4">Guía de Uso</h3>
              <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div>
                  <h4 className="text-sm font-medium text-gray-900 mb-2">Interpretación del Diagrama</h4>
                  <ul className="list-disc list-inside space-y-1 text-sm text-gray-600">
                    <li>La barra azul clara representa la duración total de cada tarea</li>
                    <li>El color dentro de la barra indica el progreso actual</li>
                    <li>Verde (80-100%): Tarea casi completada o completada</li>
                    <li>Amarillo (50-79%): Tarea en progreso saludable</li>
                    <li>Rojo (0-49%): Tarea con bajo progreso o retrasada</li>
                  </ul>
                </div>
                <div>
                  <h4 className="text-sm font-medium text-gray-900 mb-2">Recomendaciones</h4>
                  <ul className="list-disc list-inside space-y-1 text-sm text-gray-600">
                    <li>Actualice regularmente el progreso de las tareas</li>
                    <li>Revise las tareas con progreso rojo para identificar riesgos</li>
                    <li>Use esta vista para planificar sesiones de seguimiento</li>
                    <li>Ajuste las fechas de inicio y fin según el avance real</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        )}
      </main>
      {/* Modals */}
      {showAddProject && (
        <div className="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50 flex items-center justify-center p-4">
          <div className="w-full max-w-2xl">
            <ProjectForm 
              onSave={addProject} 
              onCancel={() => setShowAddProject(false)} 
            />
          </div>
        </div>
      )}
      {editingProject && (
        <div className="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50 flex items-center justify-center p-4">
          <div className="w-full max-w-2xl">
            <ProjectForm 
              project={editingProject} 
              onSave={updateProject} 
              onCancel={() => setEditingProject(null)} 
            />
          </div>
        </div>
      )}
      {selectedProject && (
        <div className="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50 flex items-center justify-center p-4">
          <div className="w-full max-w-2xl">
            <ProjectDetails 
              project={selectedProject} 
              onClose={() => setSelectedProject(null)} 
            />
          </div>
        </div>
      )}
      {showAddSession && (
        <div className="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50 flex items-center justify-center p-4">
          <div className="w-full max-w-md">
            <SessionForm 
              onSave={addSession} 
              onCancel={() => setShowAddSession(false)} 
            />
          </div>
        </div>
      )}
      {editingSession && (
        <div className="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50 flex items-center justify-center p-4">
          <div className="w-full max-w-md">
            <SessionForm 
              session={editingSession} 
              onSave={updateSession} 
              onCancel={() => setEditingSession(null)} 
            />
          </div>
        </div>
      )}
      {selectedMember && (
        <div className="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50 flex items-center justify-center p-4">
          <div className="w-full max-w-2xl">
            <AssignmentDetails 
              member={selectedMember} 
              onClose={() => setSelectedMember(null)} 
            />
          </div>
        </div>
      )}
      {showAddTask && selectedProject && (
        <div className="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50 flex items-center justify-center p-4">
          <div className="w-full max-w-md">
            <TaskForm 
              onSave={addTask} 
              onCancel={() => {
                setShowAddTask(false);
                setSelectedProject(null);
              }} 
              projectId={selectedProject.id}
            />
          </div>
        </div>
      )}
      {editingTask && selectedProject && (
        <div className="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50 flex items-center justify-center p-4">
          <div className="w-full max-w-md">
            <TaskForm 
              task={editingTask}
              onSave={updateTask} 
              onCancel={() => {
                setEditingTask(null);
                setSelectedProject(null);
              }} 
              projectId={selectedProject.id}
            />
          </div>
        </div>
      )}
      {showAddMember && (
        <div className="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50 flex items-center justify-center p-4">
          <div className="w-full max-w-2xl">
            <MemberForm 
              onSave={addMember} 
              onCancel={() => setShowAddMember(false)} 
            />
          </div>
        </div>
      )}
      {editingMember && (
        <div className="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50 flex items-center justify-center p-4">
          <div className="w-full max-w-2xl">
            <MemberForm 
              member={editingMember}
              onSave={updateMember} 
              onCancel={() => setEditingMember(null)} 
            />
          </div>
        </div>
      )}
      {/* Footer */}
      <footer className="bg-white border-t border-gray-200 mt-12">
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
          <div className="flex justify-between items-center">
            <div className="text-sm text-gray-500">
              © 2025 Dashboard de Gestión de Proyectos. Todos los derechos reservados.
            </div>
            <div className="flex space-x-6">
              <button 
                onClick={() => {
                  const data = { projects, sessions, teamMembers };
                  const dataStr = JSON.stringify(data, null, 2);
                  const dataUri = 'application/json;charset=utf-8,'+ encodeURIComponent(dataStr);
                  const exportFileDefaultName = 'dashboard-data.json';
                  const linkElement = document.createElement('a');
                  linkElement.setAttribute('href', dataUri);
                  linkElement.setAttribute('download', exportFileDefaultName);
                  linkElement.click();
                }}
                className="text-sm text-gray-500 hover:text-gray-700"
              >
                <Download className="h-5 w-5 inline mr-1" />
                Exportar Datos
              </button>
              <button 
                onClick={() => {
                  if (navigator.share) {
                    navigator.share({
                      title: 'Dashboard de Gestión de Proyectos',
                      text: 'Revisa el estado actual de nuestros proyectos y asignaciones',
                      url: window.location.href
                    });
                  } else {
                    alert('La función de compartir no está disponible en tu navegador. Copia la URL para compartir.');
                  }
                }}
                className="text-sm text-gray-500 hover:text-gray-700"
              >
                <Share2 className="h-5 w-5 inline mr-1" />
                Compartir
              </button>
            </div>
          </div>
        </div>
      </footer>
    </div>
  );
};

export default App;
