<script lang="ts">
    import axios from 'axios';
    import { onMount } from 'svelte';
    import { Button } from '$lib/components/ui/button';
    import { Card } from '$lib/components/ui/card';
    import { Tabs, TabsContent, TabsList, TabsTrigger } from '$lib/components/ui/tabs';
    import { Dialog, DialogContent, DialogHeader, DialogTitle } from '$lib/components/ui/dialog';

    interface Log {
        id: number;
        timestamp: string;
        request: string;
        response: string;
        upvotes: number;
        downvotes: number;
    }

    let logs: Log[] = [];
    let activeTab: 'pending' | 'upvoted' | 'downvoted' = 'pending';
    let showPreview = false;
    let selectedResponse = '';

    // Configure axios base URL
    const api = axios.create({
        baseURL: 'http://localhost:8000' // FastAPI server URL
    });

    onMount(async () => {
        try {
            const response = await api.get('/logs');
            logs = response.data;
        } catch (error) {
            console.error('Error fetching logs:', error);
        }
    });

    async function vote(logId: number, voteType: 'upvote' | 'downvote') {
        try {
            await api.post(`/vote/${logId}/${voteType}`);
            // Refresh logs after voting
            const response = await api.get('/logs');
            logs = response.data;
        } catch (error) {
            console.error('Error voting:', error);
        }
    }

    function showResponsePopup(encodedResponse: string) {
        try {
            // Replace URL-safe characters back to standard base64
            const base64 = encodedResponse.replace(/-/g, '+').replace(/_/g, '/');
            // Add padding if needed
            const padded = base64.padEnd(base64.length + (4 - (base64.length % 4)) % 4, '=');
            selectedResponse = JSON.stringify(JSON.parse(atob(padded)), null, 2);
            showPreview = true;
        } catch (error) {
            console.error('Error decoding response:', error);
            selectedResponse = 'Error decoding response';
            showPreview = true;
        }
    }

    function handleTabChange(value: string | undefined) {
        if (value && (value === 'pending' || value === 'upvoted' || value === 'downvoted')) {
            activeTab = value;
        }
    }

    $: pendingLogs = logs.filter((log) => log.upvotes === 0 && log.downvotes === 0);
    $: upvotedLogs = logs.filter((log) => log.upvotes > log.downvotes);
    $: downvotedLogs = logs.filter((log) => log.downvotes > log.upvotes);
</script>

<div class="bg-blue-600 text-white text-center py-2">
    <h1 class="text-xl font-bold">ATDev AI Admin</h1>
</div>

<div class="container mx-auto py-4">
    <h1 class="text-3xl font-bold mb-4 text-blue-800">Response Voting</h1>

    <Tabs value={activeTab} onValueChange={handleTabChange}>
        <TabsList>
            <TabsTrigger value="pending">Pending</TabsTrigger>
            <TabsTrigger value="upvoted">Upvoted</TabsTrigger>
            <TabsTrigger value="downvoted">Downvoted</TabsTrigger>
        </TabsList>

        <TabsContent value="pending">
            <Card>
                <table class="min-w-full divide-y divide-gray-200">
                    <thead class="bg-blue-50">
                        <tr>
                            <th class="px-6 py-3 text-left text-xs font-medium text-blue-500 uppercase tracking-wider">ID</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-blue-500 uppercase tracking-wider">Timestamp</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-blue-500 uppercase tracking-wider">Request</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-blue-500 uppercase tracking-wider">Response</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-blue-500 uppercase tracking-wider">Actions</th>
                        </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200">
                        {#each pendingLogs as log}
                            <tr>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{log.id}</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{new Date(log.timestamp).toLocaleString()}</td>
                                <td class="px-6 py-4 text-sm text-gray-500">{log.request}</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                                    <Button variant="default" on:click={() => showResponsePopup(log.response)}>
                                        <i class="fas fa-code mr-1"></i> View
                                    </Button>
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                                    <Button variant="default" class="bg-green-600 hover:bg-green-700 mr-2" on:click={() => vote(log.id, 'upvote')}>
                                        <i class="fas fa-thumbs-up"></i>
                                    </Button>
                                    <Button variant="default" class="bg-red-600 hover:bg-red-700" on:click={() => vote(log.id, 'downvote')}>
                                        <i class="fas fa-thumbs-down"></i>
                                    </Button>
                                </td>
                            </tr>
                        {/each}
                    </tbody>
                </table>
            </Card>
        </TabsContent>

        <TabsContent value="upvoted">
            <Card>
                <table class="min-w-full divide-y divide-gray-200">
                    <thead class="bg-green-50">
                        <tr>
                            <th class="px-6 py-3 text-left text-xs font-medium text-green-500 uppercase tracking-wider">ID</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-green-500 uppercase tracking-wider">Timestamp</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-green-500 uppercase tracking-wider">Request</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-green-500 uppercase tracking-wider">Response</th>
                        </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200">
                        {#each upvotedLogs as log}
                            <tr>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{log.id}</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{new Date(log.timestamp).toLocaleString()}</td>
                                <td class="px-6 py-4 text-sm text-gray-500">{log.request}</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                                    <Button variant="default" on:click={() => showResponsePopup(log.response)}>
                                        <i class="fas fa-code mr-1"></i> View
                                    </Button>
                                </td>
                            </tr>
                        {/each}
                    </tbody>
                </table>
            </Card>
        </TabsContent>

        <TabsContent value="downvoted">
            <Card>
                <table class="min-w-full divide-y divide-gray-200">
                    <thead class="bg-red-50">
                        <tr>
                            <th class="px-6 py-3 text-left text-xs font-medium text-red-500 uppercase tracking-wider">ID</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-red-500 uppercase tracking-wider">Timestamp</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-red-500 uppercase tracking-wider">Request</th>
                            <th class="px-6 py-3 text-left text-xs font-medium text-red-500 uppercase tracking-wider">Response</th>
                        </tr>
                    </thead>
                    <tbody class="bg-white divide-y divide-gray-200">
                        {#each downvotedLogs as log}
                            <tr>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{log.id}</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">{new Date(log.timestamp).toLocaleString()}</td>
                                <td class="px-6 py-4 text-sm text-gray-500">{log.request}</td>
                                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                                    <Button variant="default" on:click={() => showResponsePopup(log.response)}>
                                        <i class="fas fa-code mr-1"></i> View
                                    </Button>
                                </td>
                            </tr>
                        {/each}
                    </tbody>
                </table>
            </Card>
        </TabsContent>
    </Tabs>
</div>

<Dialog bind:open={showPreview}>
    <DialogContent>
        <DialogHeader>
            <DialogTitle>Response Preview</DialogTitle>
        </DialogHeader>
        <pre class="language-json bg-gray-100 p-4 rounded-lg overflow-auto max-h-[60vh]">
            {selectedResponse}
        </pre>
    </DialogContent>
</Dialog>

<svelte:head>
    <!-- Add FontAwesome for icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" />
    <!-- Add Highlight.js for syntax highlighting -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.5.0/styles/default.min.css" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.5.0/highlight.min.js"></script>
</svelte:head>
