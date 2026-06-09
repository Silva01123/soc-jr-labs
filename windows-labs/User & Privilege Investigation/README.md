C:\Users\Sant'Ana>whoami
pavilionhpvs\sant'ana

C:\Users\Sant'Ana>net user

Contas de usuário para \\PAVILIONHPVS

-------------------------------------------------------------------------------
Administrador            Convidado                DefaultAccount
Sant'Ana                 WDAGUtilityAccount
Comando concluído com êxito.


C:\Users\Sant'Ana>net user "Sant'Ana"
Nome de usuário                     Sant'Ana
Nome completo
Comentário
Comentário do usuário
Código do país/região               000 (Padrão do sistema)
Conta ativa                         Sim
Conta expira em                     Nunca

Última definição de senha           21/08/2024 21:41:08
A senha expira                      Nunca
Alteração de senha                  21/08/2024 21:41:08
Senha requerida                     Não
O usuário pode alterar a senha      Sim

Estações de trabalho permitidas     Todos
Script de logon
Perfil do usuário
Pasta base
Último logon                        08/06/2026 19:44:31

Horário de logon permitido          Todos

Associações de Grupo Local          *Administradores
Associações de Grupo Global         *None
Comando concluído com êxito.


C:\Users\Sant'Ana>whoami groups
ERRO: Argumento/opção inválido - 'groups'.
Digite "WHOAMI /?" para obter detalhes sobre o uso.

C:\Users\Sant'Ana>whoami /groups

INFORMAÇÕES DE GRUPO
---------------------

Nome do grupo                                                  Tipo                     SID          Atributos
============================================================== ======================== ============ ====================================================
Todos                                                          Grupo bastante conhecido S-1-1-0      Grupo obrigatório, Ativado por padrão, Grupo ativado
AUTORIDADE NT\Conta local e membro do grupo de Administradores Grupo bastante conhecido S-1-5-114    Grupo usado apenas para negar
BUILTIN\Administradores                                        Alias                    S-1-5-32-544 Grupo usado apenas para negar
BUILTIN\Usuários                                               Alias                    S-1-5-32-545 Grupo obrigatório, Ativado por padrão, Grupo ativado
AUTORIDADE NT\INTERATIVO                                       Grupo bastante conhecido S-1-5-4      Grupo obrigatório, Ativado por padrão, Grupo ativado
LOGON de CONSOLE                                               Grupo bastante conhecido S-1-2-1      Grupo obrigatório, Ativado por padrão, Grupo ativado
AUTORIDADE NT\Usuários autenticados                            Grupo bastante conhecido S-1-5-11     Grupo obrigatório, Ativado por padrão, Grupo ativado
AUTORIDADE NT\Esta organização                                 Grupo bastante conhecido S-1-5-15     Grupo obrigatório, Ativado por padrão, Grupo ativado
AUTORIDADE NT\Conta local                                      Grupo bastante conhecido S-1-5-113    Grupo obrigatório, Ativado por padrão, Grupo ativado
LOCAL                                                          Grupo bastante conhecido S-1-2-0      Grupo obrigatório, Ativado por padrão, Grupo ativado
AUTORIDADE NT\Autenticação NTLM                                Grupo bastante conhecido S-1-5-64-10  Grupo obrigatório, Ativado por padrão, Grupo ativado
Rótulo Obrigatório\Nível Obrigatório Médio                     Rótulo                   S-1-16-8192

C:\Users\Sant'Ana>net localgroup Administradores
Nome de alias      Administradores
Comentário         Os administradores têm acesso completo e irrestrito ao computador/domínio

Membros

-------------------------------------------------------------------------------
Administrador
Sant'Ana
Comando concluído com êxito.
